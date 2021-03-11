---
description: I flussi di lavoro DRM comprendono la creazione di pacchetti dei contenuti, la concessione di licenze per i contenuti e la riproduzione dei contenuti protetti dalla propria applicazione video. Il flusso di lavoro è generalmente simile per ogni soluzione DRM, ma con alcune differenze è nei dettagli.
title: Flusso di lavoro multi-DRM per FairPlay
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---


# Flusso di lavoro Multi-DRM per FairPlay {#multi-drm-workflow-for-fairplay}

I flussi di lavoro DRM comprendono la creazione di pacchetti dei contenuti, la concessione di licenze per i contenuti e la riproduzione dei contenuti protetti dalla propria applicazione video. Il flusso di lavoro è generalmente simile per ogni soluzione DRM, ma con alcune differenze è nei dettagli.

Questo flusso di lavoro Multi-DRM ti porta attraverso la configurazione, il packaging, la licenza e la riproduzione di contenuti HLS protetti con Apple FairPlay. Questo flusso di lavoro include anche istruzioni facoltative per l&#39;implementazione della riproduzione offline e della rotazione delle licenze.

## Abilita il servizio ExpressPlay per FairPlay {#enable-expressplay-service-for-fairplay}

La soluzione FairPlay DRM di Apple richiede una certa configurazione quando la si utilizza con i servizi DRM ExpressPlay. Ciò comporta l’ottenimento delle credenziali da Apple e il loro caricamento su ExpressPlay.

Segui questi passaggi per abilitare il servizio ExpressPlay per la protezione dei contenuti FairPlay.

1. Ottieni le credenziali da Apple.

   Queste credenziali vengono fornite in modo univoco a ogni provider di servizi. È necessario richiederli compilando il seguente modulo: [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >Selezionare **[!UICONTROL Content Provider]** per Ruolo principale.

   Una volta approvata la tua richiesta, Apple ti invierà un *pacchetto di distribuzione per streaming FairPlay*.
1. Genera una richiesta di firma del certificato.

   Puoi utilizzare [!DNL openssl] per generare la coppia di chiavi pubblica/privata e la richiesta di firma del certificato (CSR, Certificate signed Request).

   1. Genera la tua coppia di chiavi.

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. Genera la tua CSR.

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >Le istruzioni per questo passaggio si trovano nel *pacchetto di distribuzione dello streaming FairPlay*, ma sono incluse qui per comodità. In caso di problemi con questa parte del processo, controlla le istruzioni in *FairPlayCertificateCreation.pdf* (nel pacchetto di distribuzione).

1. Carica la tua CSR tramite il portale per sviluppatori Apple.
   1. L&#39;agente del team di sviluppo deve accedere a [!DNL developer.apple.com/account].
   1. Fai clic su **[!UICONTROL Certificates, Identifiers & Profiles]**, quindi seleziona il menu a discesa **[!UICONTROL iOS, tvOS, watchOS]** in alto a sinistra della pagina, quindi fai clic su **[!UICONTROL Certificates->Production]** a sinistra della pagina.
   1. Fai clic sul pulsante **[!UICONTROL +]** in alto a destra della pagina per richiedere un nuovo certificato. Selezionare l&#39;opzione **[!UICONTROL FairPlay Streaming Certificate]** in **[!UICONTROL Production]**.

      Viene visualizzata la finestra di dialogo *Aggiungi certificato iOS* .
   1. In *Aggiungi certificato iOS*, carica il file CSR generato nel passaggio 2.b e fai clic su **[!UICONTROL Generate]**.

      La chiave del segreto dell&#39;applicazione (ASK) viene visualizzata nella stessa finestra di dialogo.
   1. Annota la tua richiesta e la immagazzini in un luogo sicuro.
   1. Nella richiesta di informazioni per completare la generazione del certificato, fai clic su **[!UICONTROL Continue]**.
   1. Dopo aver verificato di aver salvato la richiesta, fai clic su **[!UICONTROL Generate]** per continuare.

      >[!NOTE]
      >
      >È importante salvare una copia della richiesta e archiviarla in modo sicuro. *Se la richiesta viene compromessa, non potrai più proteggere i contenuti con FairPlay Streaming.* Al team è assegnato un solo (1) ASK. Il valore non verrà più fornito e non sarà possibile recuperarlo in un secondo momento.

   1. Scarica il certificato FPS.

      Assicurati di salvare una copia di backup della tua chiave privata (dal passaggio 2.a.) e della tua chiave pubblica (il certificato FPS scaricato in questo passaggio) in un luogo sicuro.
1. Imposta il tuo account ExpressPlay con le tue credenziali FairPlay.
   1. Diciamo il nome del certificato scaricato al passaggio 3.h. è [!DNL fairplay.cer].
   1. Apri il file [!DNL fairplay.cer] con l&#39;utility Apple Keychain Access.
   1. Filtra i tuoi molti certificati immettendo &quot; `fairplay`&quot; nel campo di ricerca in alto a destra.
   1. Identifica il certificato FairPlay della tua azienda.

      Il nome dell’azienda deve essere associato al certificato rilasciato da Apple.
   1. Espandi il certificato selezionando la freccia di espansione e fai clic con il pulsante destro del mouse sulla chiave privata.
   1. Selezionare **[!UICONTROL Export "Your Company Name"]** e salvare il file [!DNL .p12].

      Ti verrà chiesto di assegnare una password per proteggere questo file. Prendi nota di questa password in quanto dovrai inviarla con il pacchetto di credenziali.
   1. Accedi al tuo account su [www.expressplay.com](https://www.expressplay.com).
   1. Fai clic su **[!UICONTROL DRM SERVICES]** in alto a sinistra, quindi seleziona la scheda **[!UICONTROL FairPlay]** .
   1. Carica le credenziali FairPlay sul tuo account ExpressPlay.

      1. Crea un file di testo che contiene il valore dell&#39;ASK (deve essere composto da 32 caratteri, ad esempio: `1234567890abcdef1234567890abcdef`) e seleziona questo file per il caricamento.
      1. Selezionare il file PKCS12 dal passaggio 4.f. per il caricamento.
      1. Immetti la password del file PKCS12 dal passaggio 4.f.
      1. Fai clic sul pulsante Carica .

Ora è possibile creare applicazioni iOS o pagine HTML5 con la protezione dei contenuti FairPlay insieme al certificato [!DNL fairplay.cer] utilizzando il servizio ExpressPlay per FairPlay.

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### Crea un pacchetto per FairPlay {#package-your-content-for-fairplay}

Per creare pacchetti dei contenuti, è possibile utilizzare Adobe Offline Packager o altri strumenti come il packager Bento4 di ExpressPlay.

I pacchetti preparano il video per la riproduzione (ad esempio, frammentando il file originale e inserendolo in un manifesto) e lo proteggono con la soluzione DRM scelta (in questo caso FairPlay):

* [Pacchetto offline di Adobe per FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [Pacchetti ExpressPlay - Bento4 per HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. Crea un pacchetto per il contenuto.

   Ecco un esempio di packaging che utilizza Adobe Offline Packager. Il Packager utilizza un file di configurazione (ad esempio, [!DNL fairplay.xml]) simile al seguente:

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

   * `in_path` - Questa voce indica la posizione del video di origine sulla macchina da imballaggio locale.
   * `out_type` - Questa voce descrive il tipo di output imballato, in questo caso HLS for FairPlay.
   * `out_path` - La posizione sul computer locale in cui si desidera che l&#39;output venga trasmesso.
   * `drm_sys` - La soluzione DRM per la quale stai effettuando il packaging. Questo è `FAIRPLAY` in questo caso.
   * `frag_dur` - Durata del frammento in secondi.
   * `target_dur` - La durata del target per l&#39;output HLS.
   * `key_file_path` - Questo è il percorso del file di licenza sul computer di imballaggio che funge da chiave di crittografia del contenuto (CEK). Si tratta di una stringa esadecimale con codifica Base-64 a 16 byte.
   * `iv_file_path` - Questa è la posizione del file IV sulla vostra macchina di imballaggio.
   * `key_url` - Il parametro URI del  `EXT-X-KEY` tag del  [!DNL .m3u8] file.
   * `content_id` - Valore predefinito.

   Come indicato nella [Documentazione di Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7), &quot;Come best practice, crea un file di configurazione che contiene le opzioni comuni che desideri utilizzare per generare gli output. Quindi, crea l&#39;output fornendo opzioni specifiche come argomento della riga di comando.&quot;

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   Il file M3U8 generato ha un attributo `EXT-X-KEY` che viene visualizzato come segue:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### Impostazione dei criteri per FairPlay {#setting-policies-for-fairplay}

È possibile impostare criteri per i contenuti protetti da FairPlay utilizzando un server di adesione. Puoi impostare un server di adesione di esempio personalizzato o utilizzare un server di adesione di esempio fornito da Adobe.

L&#39;Adobe fornisce un esempio di server di adesione ExpressPlay (SEES) che mostra come eseguire l&#39;adesione *temporizzata* e *dispositivo-binding*. Questo server di adesione di esempio è basato sui servizi ExpressPlay.

[Server di riferimento: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [Servizio di riferimento: Adesione basata sul tempo](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [Servizio di riferimento: Diritto di associazione ai dispositivi](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## Licenze e riproduzione per FairPlay {#licensing-and-playback-for-fairplay}

La concessione di licenze e la riproduzione di contenuti protetti da FairPlay richiede lo scambio di schemi URL tra lo schema utilizzato nel file manifesto video (skd:) e quello utilizzato nelle richieste di token ExpressPlay (https:).

Le istruzioni per l’implementazione delle licenze e della riproduzione da un client TVSDK iOS sono disponibili qui: [Abilita Apple FairPlay nelle applicazioni TVSDK](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md). È inoltre possibile implementare la riproduzione offline e la rotazione delle licenze per FairPlay.

## HLS offline con FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

È possibile consentire agli utenti di riprodurre contenuti protetti da FairPlay quando la relativa licenza non è recuperabile perché il lettore è isolato dal web (ad esempio su un aeroplano).

Prima di iniziare questa attività, scarica e leggi il documento Apple **&quot;Riproduzione offline con FairPlay Streaming e HTTP Live Streaming&quot;**. Leggi la guida per scoprire come scaricare i segmenti Transport Stream (TS) e salvarli nel computer locale.

Implementa la riproduzione offline per FairPlay con questo flusso di lavoro:

1. Scarica il segmento HLS TS.
1. Richiedi la licenza di noleggio permanente dal server FairPlay (vedi **&quot;FairPlay Persistent Rental Policy&quot;**).
1. Salva il `persistentContentKey`.
1. Riproduci il contenuto FairPlay offline.

>[!NOTE]
>
>FairPlay Streaming sul client non avvia la decrittografia se la chiave di contenuto persistente è scaduta. Tuttavia, se la chiave di contenuto scade durante la riproduzione, continuerà l’esperienza utente.
>
>Per ulteriori informazioni, consulta il documento [Utilizzo di HTTP Live Streaming](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) .

### Rotazione licenza FairPlay {#section_D32AA08C61474B4F876AC2A5F18CB879}

La rotazione delle licenze è uno schema per impedire l&#39;hacking delle licenze dei contenuti che vengono riprodotti per un lungo periodo di tempo.

In un manifesto M3U8, ogni tag chiave verrà applicato ai seguenti segmenti TS fino al tag chiave successivo, o fino alla fine del file.

Per aggiungere la rotazione delle licenze, procedi come segue:

* Inserire un nuovo tag chiave FairPlay durante il tempo di rotazione della licenza.

   È possibile aggiungere qualsiasi numero di tag chiave.

   Per i contenuti lineari, assicurati di mantenere il tag chiave più recente nella finestra M3U8. iOS richiederà il successivo M3U8 quando rimangono circa due segmenti TS da riprodurre (circa 20 secondi). Se il nuovo M3U8 contiene nuovi tag chiave, tutte le richieste chiave verranno eseguite immediatamente. Le chiavi esistenti precedenti non verranno più richieste. iOS attenderà il completamento di tutte le richieste chiave prima che la riproduzione venga avviata.

   Per i contenuti VOD con rotazione della licenza, tutte le richieste chiave verranno effettuate all&#39;inizio della riproduzione.

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
