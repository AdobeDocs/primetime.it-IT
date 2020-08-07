---
description: Per testare la soluzione DRM, è necessaria un'applicazione video in grado di elaborare la particolare soluzione DRM con cui si sta lavorando. Questo lettore può essere un lettore di esempio reso disponibile dal  Adobe o dalla propria applicazione video basata su TVSDK.
seo-description: Per testare la soluzione DRM, è necessaria un'applicazione video in grado di elaborare la particolare soluzione DRM con cui si sta lavorando. Questo lettore può essere un lettore di esempio reso disponibile dal  Adobe o dalla propria applicazione video basata su TVSDK.
seo-title: Riproduzione dei contenuti protetti
title: Riproduzione dei contenuti protetti
uuid: 84f73ee7-43d0-481c-a5e7-14f92169323c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# Riproduzione dei contenuti protetti {#playback-your-protected-content}

Per testare la soluzione DRM, è necessaria un&#39;applicazione video in grado di elaborare la particolare soluzione DRM con cui si sta lavorando. Questo lettore può essere un lettore di esempio reso disponibile dal  Adobe o dalla propria applicazione video basata su TVSDK.

1. Utilizzate l&#39;URL del server licenze dalla risposta token ricevuta dal server ExpressPlay per verificare se potete riprodurre il contenuto protetto.

   * **Widevine** - Utilizza la risposta Widevine direttamente come ricevuta dalla richiesta di token di licenza ExpressPlay.
   * **PlayReady** - Ottenete l&#39;URL e il token del server licenze dall&#39;oggetto JSON restituito dalla richiesta del token di licenza.
   * **FairPlay** - Utilizzate la risposta FairPlay direttamente come ricevuto dalla richiesta di token di licenza ExpressPlay.

1. Verificare la riproduzione del contenuto protetto utilizzando un lettore personalizzato o un lettore di Adobe  esistente.

   Fornite l&#39;URL del contenuto protetto (la posizione del manifesto M3U8 o MPD, a seconda della soluzione DRM che state testando).

   A seconda dell&#39;interfaccia fornita dal lettore con cui si effettua il test, potrebbe essere richiesto di fornire l&#39;URL della licenza e il token separati come stringhe nei campi di input, o come oggetto JSON incollato in una casella di testo, o forse come parametro di query nell&#39;URL.

   Alcune possibilità per i lettori di prova sono elencate qui:

   * Lettore di riferimento HTML5:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Lettore TVSDK di esempio (in fase di sviluppo) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Controllo della riproduzione durante il test della configurazione di FairPlay:** FairPlay richiede alcuni passaggi aggiuntivi per riprodurre il contenuto quando si utilizzano i server delle licenze ExpressPlay. Se utilizzate [!DNL curl] per testare le connessioni (come descritto in [Licenze](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), dovete *modificare il manifesto* M3U8 (il contenuto incluso nel pacchetto) come segue:

1. Aggiungete la risposta ricevuta dalla richiesta del token di licenza al `#EXT-X-KEY:` tag nel manifesto; e
1. Modificate il protocollo di tale URL dalla risposta (ora nel manifesto), da `https://` a `skd://`.

   Ecco un esempio completo per testare la riproduzione con FairPlay, compreso il passaggio di licenza:

1. Utilizzate la richiesta di token licenza FairPlay per ottenere l&#39;URL del token di licenza. (Utilizzate il vostro Autenticatore cliente Produzione e accertatevi di usare lo stesso CEK `iv` che è stato utilizzato per creare pacchetti di contenuti FairPlay.) Eseguite il comando seguente per ottenere l&#39;URL del token di licenza per il contenuto di esempio:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Dovreste ricevere una risposta con l&#39;URL del token di licenza simile al seguente:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Inserite la risposta restituita all&#39;URL del token di licenza nel manifesto M3U8 e *modificate l&#39;URL del token di licenza in* da `sdk://` `https://`. Di seguito è riportato un esempio del tag #EXT-X-KEY nel manifesto M3U8:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >Le informazioni precedenti si applicano solo al test della configurazione FairPlay. Potrebbe non essere applicabile alla configurazione di produzione, a seconda di come si configura il gestore FairPlay. Per informazioni dettagliate, consultate [Abilitare Apple FairPlay nelle applicazioni](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) iOS.

Se il video viene riprodotto, il pacchetto e la licenza del contenuto sono stati completati correttamente. Se il video non viene riprodotto, consultate la pagina di risoluzione dei problemi per individuare eventuali soluzioni ai problemi riscontrati.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Ad esempio, di seguito è riportata la parte dell&#39;interfaccia utente del primo lettore di test riportato sopra, in cui vengono fornite le informazioni sulle licenze ottenute dal server ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
