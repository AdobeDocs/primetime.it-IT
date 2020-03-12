---
description: Per ricevere notifiche sugli aggiornamenti della cronologia, registrate i listener di eventi appropriati.
seo-description: Per ricevere notifiche sugli aggiornamenti della cronologia, registrate i listener di eventi appropriati.
seo-title: Aggiunta di listener per TimelineUpdatedEvent
title: Aggiunta di listener per TimelineUpdatedEvent
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Aggiunta di listener per TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Per ricevere notifiche sugli aggiornamenti della cronologia, registrate i listener di eventi appropriati.

Ogni volta che la timeline si aggiorna, `MediaPlayer` viene inviato `AdobePSDK.TimelineEvent` con il tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. Implementa i listener appropriati.

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

1. Registrate i listener di eventi.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

