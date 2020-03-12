---
description: Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.
seo-description: Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.
seo-title: Utilizzare i metadati temporizzati
title: Utilizzare i metadati temporizzati
uuid: 1531780f-2502-4235-818c-6c0a6bf3d348
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Utilizzare i metadati temporizzati {#use-timed-metadata}

Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.

Per utilizzare questi `PTTimedMetadata` oggetti salvati durante la riproduzione, utilizzare il dizionario salvato dagli oggetti metadati temporizzati [Store durante l&#39;invio](../../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-timed-metadata-store.md).

1. Estrarre e aggiornare il tempo di riproduzione corrente da questa notifica e individuare tutti gli `PTTimedMetadata` oggetti con orari di inizio che corrispondono al tempo di riproduzione corrente.

   È possibile utilizzare questi oggetti per completare diverse azioni.

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

1. Svuotare periodicamente `PTTimedMetadata` le istanze non aggiornate dall&#39;elenco per evitare che la memoria cresca continuamente.