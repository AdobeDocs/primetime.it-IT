---
description: Per ricevere notifiche sugli aggiornamenti della timeline, registra i listener di eventi appropriati.
title: Aggiungi listener per TimelineUpdatedEvent
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Aggiungi i listener per TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Per ricevere notifiche sugli aggiornamenti della timeline, registra i listener di eventi appropriati.

Ogni volta che la timeline viene aggiornata, il `MediaPlayer` invia `AdobePSDK.TimelineEvent` con il tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. Implementa gli ascoltatori appropriati.

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. Registra i listener di eventi.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

