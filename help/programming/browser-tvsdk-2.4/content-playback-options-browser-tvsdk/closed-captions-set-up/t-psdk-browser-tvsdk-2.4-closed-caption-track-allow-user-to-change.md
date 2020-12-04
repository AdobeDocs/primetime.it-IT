---
description: Di seguito è riportato un esempio di come un utente può selezionare una traccia di sottotitoli codificati.
seo-description: Di seguito è riportato un esempio di come un utente può selezionare una traccia di sottotitoli codificati.
seo-title: Consentire all'utente di cambiare il tracciamento
title: Consentire all'utente di cambiare il tracciamento
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Consentire all&#39;utente di modificare la traccia{#allow-the-user-to-change-the-track}

Di seguito è riportato un esempio di come un utente può selezionare una traccia di sottotitoli codificati.

1. Per visualizzare le tracce di sottotitoli codificati disponibili, utilizzare la proprietà `MediaPlayerItem.closedCaptionsTracks`.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Per impostare la traccia dei sottotitoli codificati corrente, utilizzare il metodo `MediaPlayerItem.selectClosedCaptionsTrack`.
1. Una volta preparato l&#39;elemento del lettore multimediale, recuperatelo dal lettore multimediale utilizzando il metodo ` MediaPlayer.  currentItem `.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

