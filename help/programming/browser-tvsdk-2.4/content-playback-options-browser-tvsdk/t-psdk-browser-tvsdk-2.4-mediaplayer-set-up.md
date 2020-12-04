---
description: Un oggetto MediaPlayer racchiude il comportamento e le funzionalità di un lettore multimediale.
seo-description: Un oggetto MediaPlayer racchiude il comportamento e le funzionalità di un lettore multimediale.
seo-title: Configurare MediaPlayer
title: Configurare MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Configurare MediaPlayer{#set-up-the-mediaplayer}

Un oggetto MediaPlayer racchiude il comportamento e le funzionalità di un lettore multimediale.

1. Create un&#39;istanza di `MediaPlayer` utilizzando quanto segue:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Create un&#39;istanza `MediaPlayerView`:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   dove `container` è l&#39;elemento `div` di destinazione che contiene l&#39;elemento `HTMLMediaElement`.

   Ad esempio, in una pagina HTML:

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Chiama:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Collegare l&#39;istanza `MediaPlayerView` all&#39;istanza `MediaPlayer`:

   ```js
   player.view = view;
   ```

1. Collegare l&#39;elemento `div` dei controlli personalizzati all&#39;istanza MediaPlayer.

   Ad esempio, in HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Chiama:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

L&#39;istanza `MediaPlayer` è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.
