---
description: È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all'ora di inizio.
title: Usa metadati temporizzati
exl-id: e41718e0-2b6c-4353-a365-2d84ad4ac815
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Usa metadati temporizzati {#use-timed-metadata}

È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all&#39;ora di inizio.

Per utilizzare i file salvati `PTTimedMetadata` durante la riproduzione, utilizzare il dizionario salvato da [Archivia gli oggetti metadati temporizzati durante l’invio](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md).

1. Estrarre e aggiornare il tempo di riproduzione corrente da questa notifica e trovare tutte le `PTTimedMetadata` oggetti con orari di inizio corrispondenti al tempo di riproduzione corrente.

   È possibile utilizzare questi oggetti per completare varie azioni.

   Ad esempio:

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       CMTimeRange seekableRange = self.player.seekableRange; 
       if (CMTIMERANGE_IS_VALID(seekableRange)) 
       { 
           int currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
           NSArray *allKeys = timedMetadataCollection ? [timedMetadataCollection allKeys] : [NSArray array]; 
           NSMutableArray *timedMetadatasToDelete = [[[NSMutableArray alloc] init] autorelease]; 
           int count = [allKeys count]; 
   
           for (int i=count - 1; i > -1; i--) 
           { 
              NSNumber *currTimedMetadataTime = allKeys[i]; 
              if ([currTimedMetadataTime integerValue] == currentTime) 
              { 
               /* 
                   Use the timed metadata here and remove it from the collection. 
               */ 
                NSLog (@"IN PLAYBACK TIME %i TO EXECUTE TIMEDMETADATA %@ scheduled at time %f",currentTime,currTimedMetadata.name,CMTimeGetSeconds(currTimedMetadata.time)); 
   
               PTTimedMetadata *currTimedMetadata = [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
               [timedMetadatasToDelete addObject:currTimedMetadataTime]; 
              } 
           } 
   
           for (int i=0; i<[timedMetadatasToDelete count]; i++) 
           { 
               NSNumber *timedMetadataToDelete = timedMetadatasToDelete[i]; 
               [timedMetadataCollection removeObjectForKey:timedMetadataToDelete]; 
           } 
       } 
   }
   ```

1. Svuotamento periodico non aggiornato `PTTimedMetadata` dall&#39;elenco per impedire che la memoria cresca continuamente.
