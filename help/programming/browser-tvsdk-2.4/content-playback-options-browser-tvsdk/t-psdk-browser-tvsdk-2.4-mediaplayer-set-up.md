---
description: Un oggetto MediaPlayer incapsula il comportamento e le funzionalità di un lettore multimediale.
title: Configurare MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Configurare MediaPlayer{#set-up-the-mediaplayer}

Un oggetto MediaPlayer incapsula il comportamento e le funzionalità di un lettore multimediale.

1. Crea un&#39;istanza di `MediaPlayer` utilizzando quanto segue:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Crea un&#39;istanza `MediaPlayerView`:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   dove `container` è l&#39;elemento target `div` che contiene il `HTMLMediaElement`.

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

1. Allega l&#39;istanza `MediaPlayerView` all&#39;istanza `MediaPlayer`:

   ```js
   player.view = view;
   ```

1. Allega l&#39;elemento controlli personalizzati `div` all&#39;istanza MediaPlayer.

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

L’istanza `MediaPlayer` è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.
