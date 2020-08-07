---
description: I flussi di lavoro DRM prevedono la creazione di pacchetti di contenuti, la concessione di licenze per i contenuti e la riproduzione dei contenuti protetti dall’applicazione video. Il flusso di lavoro è generalmente simile per ogni soluzione DRM, ma con alcune differenze è indicato nei dettagli.
seo-description: I flussi di lavoro DRM prevedono la creazione di pacchetti di contenuti, la concessione di licenze per i contenuti e la riproduzione dei contenuti protetti dall’applicazione video. Il flusso di lavoro è generalmente simile per ogni soluzione DRM, ma con alcune differenze è indicato nei dettagli.
seo-title: Flusso di lavoro Multi-DRM per FairPlay
title: Flusso di lavoro Multi-DRM per FairPlay
uuid: cd940a70-400c-435e-8322-55bd624164e1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---


# Flusso di lavoro Multi-DRM per FairPlay {#multi-drm-workflow-for-fairplay}

I flussi di lavoro DRM prevedono la creazione di pacchetti di contenuti, la concessione di licenze per i contenuti e la riproduzione dei contenuti protetti dall’applicazione video. Il flusso di lavoro è generalmente simile per ogni soluzione DRM, ma con alcune differenze è indicato nei dettagli.

Questo flusso di lavoro Multi-DRM consente di configurare, creare pacchetti, concedere licenze e riprodurre contenuti HLS protetti con Apple FairPlay. Questo flusso di lavoro include anche istruzioni facoltative per implementare la riproduzione offline e la rotazione della licenza.

## Abilita il servizio ExpressPlay per FairPlay {#enable-expressplay-service-for-fairplay}

La soluzione FairPlay DRM di Apple richiede una certa configurazione quando si utilizza con i servizi DRM ExpressPlay. Ciò comporta il recupero delle credenziali da Apple e il caricamento di tali credenziali in ExpressPlay.

Attenetevi a questa procedura per abilitare il servizio ExpressPlay per la protezione dei contenuti FairPlay.

1. Ottenete le credenziali da Apple.

   Queste credenziali vengono fornite in modo univoco a ciascun provider di servizi. È necessario richiederli compilando il seguente modulo: [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >Selezionare **[!UICONTROL Content Provider]** per il ruolo principale.

   Una volta approvata la richiesta, Apple invierà un pacchetto *di distribuzione* FairPlay Streaming.
1. Generare una richiesta di firma dei certificati.

   È possibile utilizzare [!DNL openssl] per generare la coppia chiave pubblica/privata e la richiesta di firma del certificato (CSR).

   1. Genera la tua coppia di chiavi.

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. Generare il CSR.

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >Le istruzioni per questo passaggio si trovano nel pacchetto *di distribuzione* FairPlay Streaming, ma sono incluse qui per comodità. In caso di problemi con questa parte del processo, controllate le istruzioni in *FairPlayCertificateCreation.pdf* (nel pacchetto di distribuzione).

1. Caricate il CSR tramite il portale per sviluppatori Apple.
   1. L&#39;agente del team di sviluppo deve effettuare l&#39;accesso [!DNL developer.apple.com/account].
   1. Fare clic su **[!UICONTROL Certificates, Identifiers & Profiles]**, quindi selezionare l&#39; **[!UICONTROL iOS, tvOS, watchOS]** elenco a discesa in alto a sinistra della pagina, quindi fare clic **[!UICONTROL Certificates->Production]** sulla sinistra della pagina.
   1. Fate clic sul **[!UICONTROL +]** pulsante in alto a destra della pagina per richiedere un nuovo certificato. Selezionare l&#39; **[!UICONTROL FairPlay Streaming Certificate]** opzione in **[!UICONTROL Production]**.

      Viene visualizzata la finestra di dialogo *Aggiungi certificato* iOS.
   1. In *Aggiungi certificato* iOS, caricate il file CSR generato al passaggio 2.b e fate clic su **[!UICONTROL Generate]**.

      La chiave ASK (Application Secret Key) viene visualizzata nella stessa finestra di dialogo.
   1. Prendete nota della vostra domanda e archiviatela in una posizione sicura.
   1. Per completare la generazione del certificato, fai clic su **[!UICONTROL Continue]**.
   1. Dopo aver verificato di aver salvato la richiesta, fate clic **[!UICONTROL Generate]** per continuare.

      >[!NOTE]
      >
      >È importante salvare una copia della richiesta e archiviarla in modo sicuro. *Se l’ASK è compromesso, non sarà più possibile proteggere i contenuti con lo streaming FairPlay.* Solo un (1) ASK è assegnato al team. Il valore non verrà più fornito e non sarà possibile recuperarlo in un secondo momento.

   1. Scaricate il certificato FPS.

      Accertatevi di salvare una copia di backup della chiave privata (dal passaggio 2.a.) e della chiave pubblica (il certificato FPS scaricato in questo passaggio) in un luogo sicuro.
1. Configurate il vostro account ExpressPlay con le vostre credenziali FairPlay.
   1. Diciamo il nome del certificato che hai scaricato al punto 3.h. è [!DNL fairplay.cer].
   1. Aprite il [!DNL fairplay.cer] file con l&#39;utility Apple Keychain Access.
   1. Filtrate i numerosi certificati immettendo &quot; `fairplay`&quot; nel campo di ricerca situato in alto a destra.
   1. Identifica il certificato FairPlay della tua azienda.

      Il nome della società deve essere associato al certificato rilasciato da Apple.
   1. Espandi il certificato selezionando la freccia di espansione e facendo clic con il pulsante destro del mouse sulla chiave privata.
   1. Selezionare **[!UICONTROL Export "Your Company Name"]** e salvare il [!DNL .p12] file.

      Vi verrà chiesto di assegnare una password per proteggere il file. Prendete nota di questa password, in quanto dovrete inviarla con il pacchetto di credenziali.
   1. Accedete al vostro account su [www.expressplay.com](https://www.expressplay.com).
   1. Fare clic **[!UICONTROL DRM SERVICES]** in alto a sinistra, quindi selezionare la **[!UICONTROL FairPlay]** scheda.
   1. Carica le tue credenziali FairPlay nel tuo account ExpressPlay.

      1. Create un file di testo che contenga il valore ASK (ad esempio, 32 caratteri): `1234567890abcdef1234567890abcdef`) e selezionate questo file per il caricamento.
      1. Selezionate il file PKCS12 dal passaggio 4.f. per il caricamento.
      1. Immettete la password del file PKCS12 dal passaggio 4.f.
      1. Fate clic sul pulsante Carica.

Ora potete creare applicazioni iOS o pagine HTML5 con la protezione del contenuto FairPlay insieme al vostro [!DNL fairplay.cer] certificato utilizzando il servizio ExpressPlay per FairPlay.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### Creazione di pacchetti di contenuti per FairPlay {#package-your-content-for-fairplay}

Per creare pacchetti di contenuti, potete utilizzare  Adobe Offline Packager o altri strumenti come ExpressPlay&#39;s Bento4 packager.

I Packager preparano il video per la riproduzione (ad esempio, frammentando il file originale e inserendolo in un manifesto) e proteggono il video con la soluzione DRM scelta (in questo caso FairPlay):

* [Adobe Offline Packager per FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [Pacchetti ExpressPlay - Bento4 per HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. Create pacchetti per il contenuto.

   Di seguito è riportato un esempio di package con  Adobe Offline Packager. Il Packager utilizza un file di configurazione (ad esempio, [!DNL fairplay.xml]) simile al seguente:

   ```
   <config>
   <in_path>mp4_file_path</in_path>
   <out_type>hls</out_type>
   <out_path>out_file_path</out_path>
   <drm/>
   <drm_sys>FAIRPLAY</drm_sys>
   <frag_dur>4</frag_dur>
   <target_dur>6</target_dur>
   <key_file_path>creds/fairplay.bin</key_file_path>
   <iv_file_path>creds/iv.bin</iv_file_path>
   <key_url>user_provided_value</key_url>
   <content_id>_default_</content_id>
   </config>
   ```

   * `in_path` - Questa voce indica la posizione del video sorgente sul computer locale di imballaggio.
   * `out_type` - Questa voce descrive il tipo di output confezionato, in questo caso HLS for FairPlay.
   * `out_path` - La posizione sul computer locale in cui si desidera che l&#39;output venga eseguito.
   * `drm_sys` - La soluzione DRM per la quale state creando un pacchetto. Questo è `FAIRPLAY` in questo caso.
   * `frag_dur` - Durata del frammento in secondi.
   * `target_dur` - La durata di destinazione per l&#39;output HLS.
   * `key_file_path` - Si tratta della posizione del file di licenza nel computer in uso che funge da chiave di crittografia del contenuto (CEK). Si tratta di una stringa esadecimale con codifica Base-64 a 16 byte.
   * `iv_file_path` - Questa è la posizione del file IV sul computer di imballaggio.
   * `key_url` - Il parametro URI del `EXT-X-KEY` tag del [!DNL .m3u8] file.
   * `content_id` - Valore predefinito.

   Come indicato nella documentazione [di](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)Packager, &quot;Come procedura ottimale, create un file di configurazione che contenga le opzioni comuni che desiderate utilizzare per generare gli output. Quindi, create l&#39;output fornendo opzioni specifiche come argomento della riga di comando.&quot;

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   Il file M3U8 generato ha un `EXT-X-KEY` attributo che viene visualizzato come segue:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### Impostazione dei criteri per FairPlay {#setting-policies-for-fairplay}

Potete impostare criteri per il contenuto protetto da FairPlay utilizzando un server di adesione. Potete configurare un server di adesione di esempio personalizzato o utilizzare un server di adesione di Adobe .

 Adobe fornisce un server di adesione ExpressPlay (SEES) di esempio che mostra come eseguire l&#39;adesione in base all&#39; *ora* e il binding *del* dispositivo. Questo server di adesione di esempio è basato sui servizi ExpressPlay.

[Server di riferimento: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [Servizio di riferimento: Adesione basata su tempo](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [Servizio di riferimento: Adesione a binding dispositivo](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## Licenze e riproduzione per FairPlay {#licensing-and-playback-for-fairplay}

La licenza e la riproduzione di contenuti protetti da FairPlay richiedono lo scambio di schemi URL tra lo schema utilizzato nel file manifesto video (skd:) e quello utilizzato nelle richieste di token ExpressPlay (https:).

Le istruzioni per implementare la licenza e la riproduzione da un client TVSDK iOS sono disponibili qui: [Abilita Apple FairPlay nelle applicazioni](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)TVSDK. È inoltre possibile implementare la riproduzione offline e la rotazione della licenza per FairPlay.

## HLS offline con FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

Potrebbe essere utile consentire agli utenti di riprodurre contenuti protetti da FairPlay quando la licenza non è recuperabile perché il lettore è isolato dal Web (ad esempio su un aereo).

Prima di iniziare questa attività, scaricate e leggete il documento Apple **&quot;Offline Playback with FairPlay Streaming and HTTP Live Streaming&quot;**. Leggi la guida per scoprire come scaricare i segmenti di Transport Stream (TS) e salvarli nel computer locale.

Implementa la riproduzione offline per FairPlay con il seguente flusso di lavoro:

1. Scaricate il segmento HLS TS.
1. Richiedete la licenza di affitto permanente dal server FairPlay (consultate **&quot;FairPlay Persistent Rental Policy&quot;**).
1. Salva il `persistentContentKey`.
1. Riproduci il contenuto FairPlay offline.

>[!NOTE]
>
>FairPlay Streaming sul client non avvia la decrittografia se la chiave di contenuto persistente è scaduta. Tuttavia, se la chiave di contenuto scade durante la riproduzione, l’utente continuerà a utilizzare la chiave.
>
>Per ulteriori informazioni, consultate [Utilizzo del documento HTTP Live Streaming](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) .

### Rotazione licenza FairPlay {#section_D32AA08C61474B4F876AC2A5F18CB879}

La rotazione delle licenze è uno schema per impedire l&#39;hacking delle licenze dei contenuti che vengono riprodotti per un periodo di tempo prolungato.

In un manifesto M3U8, ogni tag chiave verrà applicato ai seguenti segmenti TS fino al tag chiave successivo, o fino alla fine del file.

Per aggiungere la rotazione della licenza, effettuate le seguenti operazioni:

* Inserite un nuovo tag di chiave FairPlay durante il tempo di rotazione della licenza.

   È possibile aggiungere un numero qualsiasi di tag chiave.

   Per i contenuti lineari, assicurarsi di mantenere il tag chiave più recente nella finestra M3U8. iOS richiederà la successiva M3U8 quando restano circa due segmenti TS da riprodurre (circa 20 secondi). Se il nuovo M3U8 contiene nuovi tag chiave, tutte le richieste chiave verranno effettuate immediatamente. Le chiavi esistenti precedenti non saranno più richieste. iOS attenderà il completamento di tutte le richieste chiave prima dell&#39;avvio della riproduzione.

   Per i contenuti VOD con rotazione della licenza, tutte le richieste chiave si verificheranno all&#39;inizio della riproduzione.

   Di seguito è riportato un esempio M3U8 con rotazione chiave:

   ```
   #EXTM3U
   #EXT-X-TARGETDURATION:10
   #EXT-X-VERSION:5
   #EXT-X-MEDIA-SEQUENCE:0
   #EXT-X-PLAYLIST-TYPE:VOD
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://one?cek=1dc2cc71d913f4f74eca0c4632
   212b25&iv=e21f0f72b6363ff6143737cb1e9ca8d7",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence0.ts
   #EXTINF:10,
   fileSequence1.ts
   #EXTINF:10,
   fileSequence2.ts
   #EXTINF:10,
   fileSequence3.ts
   #EXTINF:10,
   fileSequence4.ts
   #EXTINF:10,
   fileSequence5.ts
   #EXTINF:10,
   fileSequence6.ts
   #EXTINF:10,
   fileSequence7.ts
   #EXTINF:10,
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://two?cek=f6efc698b96cf8f4fa46d5237d
   337c77&iv=18401077091784bcda8079acf978dc95",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence8.ts
   #EXTINF:10,
   ```
