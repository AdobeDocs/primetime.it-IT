---
description: Ecco un esempio di come un utente può selezionare una traccia a didascalia chiusa.
title: Consenti all'utente di modificare il brano
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---


# Consenti all&#39;utente di modificare la traccia{#allow-the-user-to-change-the-track}

Ecco un esempio di come un utente può selezionare una traccia a didascalia chiusa.

1. Per visualizzare le tracce di didascalia chiusa disponibili, utilizzare la proprietà `MediaPlayerItem.closedCaptionsTracks` .

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Per impostare la traccia dei sottotitoli codificati corrente, utilizzare il metodo `MediaPlayerItem.selectClosedCaptionsTrack` .
1. Una volta preparato l&#39;elemento del lettore multimediale, recuperalo dal lettore multimediale utilizzando il metodo ` MediaPlayer.  currentItem ` .

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

