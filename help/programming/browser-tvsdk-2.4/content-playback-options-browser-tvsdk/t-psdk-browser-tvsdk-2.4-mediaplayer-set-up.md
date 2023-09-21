---
description: Un oggetto MediaPlayer incapsula il comportamento e le funzionalità di un lettore multimediale.
title: Configurare MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Configurare MediaPlayer{#set-up-the-mediaplayer}

Un oggetto MediaPlayer incapsula il comportamento e le funzionalità di un lettore multimediale.

1. Crea istanza di `MediaPlayer` utilizzando quanto segue:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Creare un `MediaPlayerView` istanza:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   dove `container` è il target `div` elemento che contiene il `HTMLMediaElement`.

   Ad esempio, in una pagina di HTML:

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Chiamata:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Allega `MediaPlayerView` istanza al tuo `MediaPlayer` istanza:

   ```js
   player.view = view;
   ```

1. Allegare i controlli personalizzati `div` nell&#39;istanza MediaPlayer.

   Ad esempio, in HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Chiamata:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

Il `MediaPlayer` L’istanza di è ora disponibile e configurata correttamente per visualizzare contenuti video sullo schermo del dispositivo.
