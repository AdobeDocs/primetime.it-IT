---
description: Per ricevere notifiche sui tag nel manifesto, registra i listener di eventi appropriati.
title: Aggiungere listener per le notifiche di metadati temporizzate
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Aggiungere listener per le notifiche di metadati temporizzate{#add-listeners-for-timed-metadata-notifications}

Per ricevere notifiche sui tag nel manifesto, registra i listener di eventi appropriati.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione l’attività correlata:

* `MediaPlayerItemEvent.ITEM_CREATED`: elenco iniziale di `TimedMetadata` Gli oggetti sono disponibili dopo il `MediaPlayerItem` viene creato.

  Questo evento avvisa l&#39;applicazione quando si verifica.

* `MediaPlayerItemEvent.ITEM_UPDATED`: per i flussi live/lineari in cui il manifesto/la playlist viene aggiornato periodicamente, nella playlist/il manifesto aggiornato potrebbero essere visualizzati tag personalizzati aggiuntivi `TimedMetadata` Gli oggetti possono essere aggiunti al `MediaPlayerItem.timedMetadata` proprietà.

  Questo evento avvisa l&#39;applicazione quando si verifica.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: ogni volta che un nuovo `TimedMetadata` viene creato, l&#39;evento viene inviato da MediaPlayer.

  Questo evento non viene inviato per `TimedMetadata` oggetto creato durante la fase di inizializzazione.

1. Implementare i listener appropriati.

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

1. Registrare i listener di eventi.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

I metadati ID3 vengono inviati tramite lo stesso `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. Tuttavia, questo non dovrebbe causare confusione, perché è possibile utilizzare un oggetto TimedMetadata `type` per distinguere tra TAG e ID3. Per ulteriori informazioni sui tag ID3, consulta [Tag ID3](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
