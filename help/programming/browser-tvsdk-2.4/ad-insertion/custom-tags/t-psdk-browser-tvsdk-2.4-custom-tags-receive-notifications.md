---
description: Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.
seo-description: Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.
seo-title: Aggiunta di listener per le notifiche di metadati temporizzati
title: Aggiunta di listener per le notifiche di metadati temporizzati
uuid: c82c5549-0ab6-4343-a766-5176e784d4cb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Aggiunta di listener per le notifiche di metadati temporizzati{#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.

Quando viene creato un nuovo `TimedMetadata` oggetto, MediaPlayer invia `AdobePSDK.TimedMetadataEvent`.

1. Implementa i listener appropriati.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registrate i listener di eventi.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

I metadati ID3 vengono inviati attraverso lo stesso `Events.TimedMetadataEvent`. È possibile utilizzare la `timedMetadata.type` proprietà per distinguere tra TAG e ID3.

