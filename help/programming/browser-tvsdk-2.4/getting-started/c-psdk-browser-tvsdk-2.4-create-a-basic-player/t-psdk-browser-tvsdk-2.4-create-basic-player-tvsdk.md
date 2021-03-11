---
description: Completa i seguenti passaggi per creare un lettore di base utilizzando il browser TVSDK.
title: Creare un lettore di base utilizzando TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Creare un lettore di base utilizzando TVSDK{#create-a-basic-player-using-tvsdk}

Completa i seguenti passaggi per creare un lettore di base utilizzando il browser TVSDK.

1. Crea una nuova directory in cui puoi scaricare i file compressi per Browser TVSDK.
1. Scarica Browser TVSDK da Zendesk, decomprimi i file e inserisci la cartella dei framework nella nuova directory.
1. Crea un semplice modello HTML per il codice con un `div` al suo interno.
1. Posiziona questo modello in un file HTML nella directory creata al punto 1.

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

1. Aggiungi le librerie TVSDK per browser nella sezione head.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Per il tag body, aggiungi la sezione `onLoad` .

   ```
   <body onload="startVideo()">
   ```

1. Inizia a implementare la funzione `startVideo` .
1. Aggiungi un tag script e crea la funzione `startVideo` nel tag .

   Questo dovrebbe essere nella sezione iniziale della pagina.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Crea il `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Crea il `MediaPlayerView`.

   >[!TIP]
   >
   >In questo punto viene utilizzato il `div` creato in precedenza.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Aggiungi il listener di eventi del lettore.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementa il gestore eventi e inseriscilo prima del listener di eventi add.

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

1. Crea il `MediaResource`, che passa il collegamento M3U8 (o mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Crea una configurazione vuota e sostituisci la risorsa .

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. Quando il lettore è nello stato INITIALIZZATO, chiama `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Una volta che il lettore è nello stato PREPARATO, chiama `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

