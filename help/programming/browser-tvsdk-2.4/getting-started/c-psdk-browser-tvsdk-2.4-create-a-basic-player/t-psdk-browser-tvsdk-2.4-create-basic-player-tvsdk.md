---
description: Per creare un lettore di base utilizzando il browser TVSDK, completare i seguenti passaggi.
seo-description: Per creare un lettore di base utilizzando il browser TVSDK, completare i seguenti passaggi.
seo-title: Creazione di un lettore di base con TVSDK
title: Creazione di un lettore di base con TVSDK
uuid: ec15cf53-197f-4190-a6b2-600a57815390
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Creazione di un lettore di base con TVSDK{#create-a-basic-player-using-tvsdk}

Per creare un lettore di base utilizzando il browser TVSDK, completare i seguenti passaggi.

1. Create una nuova directory in cui scaricare i file compressi per l&#39;SDK del browser.
1. Scaricate Browser TVSDK da Zendesk, decomprimete i file e inserite la cartella framework nella nuova directory.
1. Create un semplice standard HTML per il codice con un `div` contenuto.
1. Inserite questo standard in un file HTML nella directory creata al punto 1.

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. Aggiungete le librerie TVSDK del browser nella sezione head.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Per il tag body, aggiungete la `onLoad` sezione .

   ```
   <body onload="startVideo()">
   ```

1. Iniziate ad implementare la `startVideo` funzione.
1. Aggiungete un tag script e create la `startVideo` funzione nel tag .

   Questo dovrebbe essere nella sezione head della pagina.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Create il `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Create il `MediaPlayerView`.

   >[!TIP]
   >
   >Qui vengono utilizzati i `div` dati creati in precedenza.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Aggiungete il listener di eventi del lettore.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementare il gestore eventi e posizionarlo prima del listener di eventi add.

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. Create il `MediaResource`, che passa il collegamento M3U8 (o mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Create una configurazione vuota e sostituite la risorsa.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. Quando il lettore è nello stato INITIALIZED, chiama `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Dopo che il lettore è nello stato PREPARATO, chiama `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

