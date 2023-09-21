---
description: Per testare la soluzione DRM, è necessario disporre di un'applicazione video in grado di elaborare la specifica soluzione DRM utilizzata. Questo lettore può essere un sample player reso disponibile da Adobe, o dalla tua applicazione video basata su TVSDK.
title: Riprodurre il contenuto protetto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Riprodurre il contenuto protetto {#playback-your-protected-content}

Per testare la soluzione DRM, è necessario disporre di un&#39;applicazione video in grado di elaborare la specifica soluzione DRM utilizzata. Questo lettore può essere un sample player reso disponibile da Adobe, o dalla tua applicazione video basata su TVSDK.

1. Utilizzare l&#39;URL del server licenze dalla risposta del token ottenuta dal server ExpressPlay per verificare se è possibile riprodurre il contenuto protetto.

   * **Widevine** : utilizza la risposta Widevine direttamente come ricevuta dalla richiesta del token di licenza ExpressPlay.
   * **PlayReady** - Ottieni l’URL e il token del server licenze dall’oggetto JSON restituito dalla richiesta del token di licenza.
   * **FairPlay** : utilizza la risposta FairPlay direttamente come ricevuta dalla richiesta del token di licenza ExpressPlay.

1. Verifica la riproduzione del contenuto protetto utilizzando il lettore personalizzato o un sample player di Adobe esistente.

   Fornisci l’URL del contenuto protetto (la posizione del manifesto M3U8 o MPD, a seconda della soluzione DRM che stai testando).

   A seconda dell’interfaccia fornita dal lettore su cui esegui il test, ti potrebbe essere chiesto di fornire l’URL della licenza e il token separati come stringhe nei campi di input, come oggetto JSON incollato in una casella di testo o come parametro di query nell’URL.

   Alcune possibilità per i giocatori di prova sono elencate qui:

   * Lettore di riferimento HTML5:

     ```
     https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
     ```

   * Giocatore Shaka:

     ```
     https://shaka-player-demo.appspot.com
     ```

   * Lettore TVSDK di esempio (in sviluppo) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Controllo della riproduzione durante il test della configurazione FairPlay:** FairPlay richiede alcuni passaggi aggiuntivi per riprodurre i contenuti quando si utilizzano i server di licenze ExpressPlay. Se sta usando [!DNL curl] per verificare le connessioni (come descritto in [Licenze](../../multi-drm-workflows/quick-start/handle-the-licensing.md)), è necessario *modificare il manifesto M3U8* (contenuto del pacchetto) come segue:

1. Aggiungi la risposta ottenuta dalla richiesta del token di licenza a `#EXT-X-KEY:` la marcatura nel manifesto; e
1. Modifica il protocollo di tale URL dalla risposta (ora nel manifesto), da `https://` a `skd://`.

   Di seguito è riportato un esempio completo per testare la riproduzione con FairPlay, incluso il passaggio di licenza:

1. Utilizza la richiesta del token di licenza FairPlay per ottenere l’URL del token di licenza. (Utilizza il tuo Production Customer Authenticator e assicurati di utilizzare lo stesso codice di accesso e `iv` utilizzato per creare il pacchetto dei contenuti FairPlay.) Esegui il comando seguente per ottenere l’URL del token di licenza per il contenuto di esempio:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Dovresti ricevere una risposta con l’URL del token di licenza simile al seguente:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Inserire la risposta URL del token di licenza restituito nel manifesto M3U8 e *modificare lo schema dell’URL del token di licenza in* `sdk://` da `https://`. Di seguito è riportato un esempio del tag #EXT-X-KEY nel manifesto M3U8:

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
   >Le informazioni precedenti sono valide solo per il test della configurazione di FairPlay. Potrebbe non essere applicabile alla configurazione di produzione, a seconda della modalità di configurazione del gestore FairPlay. Consulta [Abilitare Apple FairPlay nelle applicazioni iOS](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) per i dettagli.

Se il video viene riprodotto, il pacchetto e la licenza del contenuto sono stati completati. Se il video non viene riprodotto, vedere la pagina relativa alla risoluzione dei problemi per trovare alcune possibili soluzioni.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Ad esempio, la parte dell’interfaccia utente nel primo lettore di test elencato sopra, in cui fornisci le informazioni sulle licenze ottenute dal server ExpressPlay:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
