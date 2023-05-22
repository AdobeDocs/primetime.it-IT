---
description: Per creare un lettore di base utilizzando il TVSDK del browser, completa i passaggi seguenti.
title: Creare un lettore di base utilizzando TVSDK
exl-id: ea7485e0-5d15-469b-b8b6-f9604d283492
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Creare un lettore di base utilizzando TVSDK{#create-a-basic-player-using-tvsdk}

Per creare un lettore di base utilizzando il TVSDK del browser, completa i passaggi seguenti.

1. Crea una nuova directory in cui puoi scaricare i file compressi per il browser TVSDK.
1. Scarica Browser TVSDK da Zendesk, decomprimi i file e inserisci la cartella frameworks nella nuova directory.
1. Crea una semplice boilerplate HTML per il codice con un `div` in esso.
1. Posizionate questa piastra di supporto in un file HTML nella directory creata al punto 1.

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

1. Aggiungi le librerie TVSDK del browser nella sezione head.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Per il tag body, aggiungi `onLoad` sezione.

   ```
   <body onload="startVideo()">
   ```

1. Inizia a implementare `startVideo` funzione.
1. Aggiungi un tag script e crea il `startVideo` nel tag.

   Questo dovrebbe essere nella sezione head della pagina.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Creare `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Creare `MediaPlayerView`.

   >[!TIP]
   >
   >Qui è dove `div` viene utilizzato quello creato in precedenza.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Aggiungi il listener di eventi del lettore.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementa il gestore eventi e inseriscilo prima dell’aggiunta del listener di eventi.

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

1. Creare `MediaResource`, che passa il collegamento M3U8 (o mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Crea una configurazione vuota e sostituisci la risorsa.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. Quando il lettore si trova nello stato INIZIALIZZATO, chiama `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Quando il lettore è nello stato READY, chiama `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
