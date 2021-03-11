---
description: Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.
title: Aggiungi i listener per le notifiche con metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Aggiungi i listener per le notifiche con metadati temporizzati{#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, ascolta AdobePSDK.TimedMetadataEvent.

Quando viene creato un nuovo oggetto `TimedMetadata`, MediaPlayer invia `AdobePSDK.TimedMetadataEvent`.

1. Implementa gli ascoltatori appropriati.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registra i listener di eventi.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

I metadati ID3 vengono inviati attraverso lo stesso `Events.TimedMetadataEvent`. Puoi utilizzare la proprietà `timedMetadata.type` per distinguere tra TAG e ID3.

