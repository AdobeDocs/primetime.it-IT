---
description: Di seguito è riportato un esempio di come un utente può selezionare una traccia di sottotitoli.
title: Consenti all'utente di modificare il brano
exl-id: 103ca0ad-2707-4e4f-87ee-f55041e4527a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# Consenti all&#39;utente di modificare il brano{#allow-the-user-to-change-the-track}

Di seguito è riportato un esempio di come un utente può selezionare una traccia di sottotitoli.

1. Per visualizzare le tracce di sottotitoli codificati disponibili, utilizzare `MediaPlayerItem.closedCaptionsTracks` proprietà.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Per impostare la traccia con sottotitoli codificati corrente, utilizzare `MediaPlayerItem.selectClosedCaptionsTrack` metodo.
1. Dopo aver preparato l’elemento del lettore multimediale, recuperalo dal lettore utilizzando ` MediaPlayer.  currentItem ` metodo.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
