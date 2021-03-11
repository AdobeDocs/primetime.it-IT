---
description: Per ricevere notifiche sui tag nel manifesto, registra i listener di eventi appropriati.
title: Aggiungi i listener per le notifiche dei metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Aggiungi i listener per le notifiche dei metadati temporizzati{#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, registra i listener di eventi appropriati.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `MediaPlayerItemEvent.ITEM_CREATED`: L’elenco iniziale di  `TimedMetadata` oggetti è disponibile dopo la creazione  `MediaPlayerItem` di .

   Questo evento notifica l&#39;applicazione quando si verifica questa situazione.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Per i flussi in diretta/lineare in cui il manifesto/playlist si aggiorna periodicamente, potrebbero essere visualizzati tag personalizzati aggiuntivi nella playlist/manifesto aggiornato, pertanto è possibile aggiungere  `TimedMetadata` oggetti aggiuntivi alla  `MediaPlayerItem.timedMetadata` proprietà.

   Questo evento notifica l&#39;applicazione quando si verifica questa situazione.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Ogni volta che viene creato un nuovo  `TimedMetadata` oggetto, questo evento viene inviato da MediaPlayer.

   Questo evento non viene inviato per l&#39;oggetto `TimedMetadata` creato durante la fase di inizializzazione.

1. Implementa gli ascoltatori appropriati.

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

1. Registra i listener di eventi.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

I metadati ID3 vengono inviati attraverso lo stesso `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Tuttavia, questo non deve causare confusione, perché è possibile utilizzare la proprietà `type` di un oggetto TimedMetadata per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, consulta [ID3 tags](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).