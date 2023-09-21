---
description: Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.
title: Aggiungere listener per le notifiche con metadati temporizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Aggiungere listener per le notifiche con metadati temporizzati{#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.

Quando un nuovo `TimedMetadata` viene creato, MediaPlayer invia `AdobePSDK.TimedMetadataEvent`.

1. Implementare i listener appropriati.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registrare i listener di eventi.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

I metadati ID3 vengono inviati tramite lo stesso `Events.TimedMetadataEvent`. È possibile utilizzare `timedMetadata.type` per distinguere tra TAG e ID3.
