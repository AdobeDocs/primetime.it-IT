---
description: Per ricevere notifiche sui tag nel manifesto, registrare i listener di eventi appropriati.
seo-description: Per ricevere notifiche sui tag nel manifesto, registrare i listener di eventi appropriati.
seo-title: Aggiunta di listener per le notifiche di metadati temporizzate
title: Aggiunta di listener per le notifiche di metadati temporizzate
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Aggiunta di listener per le notifiche di metadati temporizzate{#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, registrare i listener di eventi appropriati.

Potete monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `MediaPlayerItemEvent.ITEM_CREATED`: L&#39;elenco iniziale di  `TimedMetadata` oggetti è disponibile dopo la creazione dell&#39; `MediaPlayerItem` oggetto.

   Questo evento notifica l’applicazione in caso di evento.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Per i flussi live/lineari in cui il manifest/playlist viene aggiornato periodicamente, è possibile che nella playlist/nel manifesto aggiornato vengano visualizzati tag personalizzati aggiuntivi, per cui è possibile aggiungere  `TimedMetadata` oggetti aggiuntivi alla  `MediaPlayerItem.timedMetadata` proprietà.

   Questo evento notifica l’applicazione in caso di evento.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Ogni volta che viene creato un nuovo  `TimedMetadata` oggetto, questo evento viene inviato da MediaPlayer.

   Questo evento non viene inviato per l&#39;oggetto `TimedMetadata` creato durante la fase di inizializzazione.

1. Implementa i listener appropriati.

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. Registrate i listener di eventi.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

I metadati ID3 vengono inviati attraverso la stessa `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Ciò non deve creare confusione, tuttavia, perché è possibile utilizzare una proprietà `type` dell&#39;oggetto TimedMetadata per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, vedere [ID3 tags](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).