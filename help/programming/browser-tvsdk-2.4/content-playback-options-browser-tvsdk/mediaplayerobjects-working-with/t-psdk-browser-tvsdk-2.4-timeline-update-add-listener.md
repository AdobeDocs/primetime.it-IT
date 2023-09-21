---
description: Per ricevere notifiche sugli aggiornamenti della timeline, registra i listener di eventi appropriati.
title: Aggiungi listener per TimelineUpdatedEvent
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Aggiungi listener per TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Per ricevere notifiche sugli aggiornamenti della timeline, registra i listener di eventi appropriati.

Ad ogni aggiornamento della timeline, `MediaPlayer` spedizioni `AdobePSDK.TimelineEvent` con tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. Implementare i listener appropriati.

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

1. Registrare i listener di eventi.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
