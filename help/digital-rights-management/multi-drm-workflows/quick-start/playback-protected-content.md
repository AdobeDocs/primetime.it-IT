---
description: Per testare la soluzione DRM, è necessaria un'applicazione video in grado di elaborare la particolare soluzione DRM con cui stai lavorando. Questo lettore può essere un sample player reso disponibile da Adobe o dalla tua applicazione video basata su TVSDK.
title: Riproduzione di contenuti protetti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Riproduzione dei contenuti protetti {#playback-your-protected-content}

Per testare la soluzione DRM, è necessaria un&#39;applicazione video in grado di elaborare la particolare soluzione DRM con cui stai lavorando. Questo lettore può essere un sample player reso disponibile da Adobe o dalla tua applicazione video basata su TVSDK.

1. Utilizza l&#39;URL del server licenze dalla risposta token ricevuta dal server ExpressPlay per verificare se è possibile riprodurre il contenuto protetto.

   * **Widevine**  - Utilizza la risposta Widevine direttamente come ricevuto dalla tua richiesta di token di licenza ExpressPlay.
   * **PlayReady**  - Ottieni l’URL e il token del server licenze dall’oggetto JSON restituito dalla richiesta del token di licenza.
   * **FairPlay**  - Utilizza la risposta FairPlay direttamente come ricevuto dalla richiesta di token di licenza ExpressPlay.

1. Verificare la riproduzione dei contenuti protetti utilizzando il proprio lettore o un lettore di Adobe esistente.

   Fornisci l&#39;URL del contenuto protetto (la posizione del manifesto M3U8 o MPD, a seconda della soluzione DRM che stai testando).

   A seconda dell’interfaccia fornita dal lettore con cui si esegue il test, potrebbe essere richiesto di fornire l’URL della licenza e il token separati come stringhe nei campi di input, o come oggetto JSON incollato in una casella di testo, o forse come parametro di query nell’URL.

   Alcune possibilità per i giocatori di prova sono elencate qui:

   * Lettore di riferimento HTML5:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Giocatore di Shaka:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Lettore TVSDK di esempio (in fase di sviluppo) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Controllo della riproduzione durante il test della configurazione FairPlay:** FairPlay richiede alcuni passaggi aggiuntivi per riprodurre il contenuto quando si utilizzano i server di licenze ExpressPlay. Se utilizzi [!DNL curl] per testare le connessioni (come descritto in [Licenze](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), devi *modificare il manifesto M3U8* (il contenuto incluso nel pacchetto) come segue:

1. Aggiungi la risposta ricevuta dalla richiesta del token di licenza al tag `#EXT-X-KEY:` nel manifesto; e
1. Modifica il protocollo di tale URL dalla risposta (ora nel manifesto), da `https://` a `skd://`.

   Ecco un esempio completo per testare la riproduzione con FairPlay, incluso il passaggio di licenza:

1. Utilizza la richiesta del token di licenza FairPlay per ottenere l’URL del token di licenza. (Utilizza il tuo Autenticatore del cliente di produzione e assicurati di utilizzare gli stessi CEK e `iv` utilizzati per creare pacchetti di contenuti FairPlay.) Esegui il comando seguente per ottenere l’URL del token di licenza per il contenuto dell’esempio:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Dovresti ricevere una risposta con l’URL del token di licenza che assomiglia a questo:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Inserisci la risposta dell’URL del token di licenza nel manifesto M3U8 e *modifica lo schema dell’URL del token di licenza in* `sdk://` da `https://`. Di seguito è riportato un esempio del tag #EXT-X-KEY nel manifesto M3U8:

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
   >Le informazioni precedenti si applicano solo al test della configurazione FairPlay. Potrebbe non essere applicabile alla configurazione di produzione, a seconda di come si configura il gestore FairPlay. Per ulteriori informazioni, consulta [Abilita Apple FairPlay nelle applicazioni iOS](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) .

Se il video viene riprodotto, il contenuto è stato compilato e concesso in licenza. Se il video non viene riprodotto, controlla nella pagina di risoluzione dei problemi alcune possibili soluzioni ai problemi.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Ad esempio, qui è la parte dell&#39;interfaccia utente nel primo lettore di test elencato sopra, dove si forniscono le informazioni sulle licenze ottenute dal server ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
