---
description: È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all'ora di inizio.
title: Utilizzare i metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# Usa metadati temporizzati{#use-timed-metadata}

È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all&#39;ora di inizio.

Per utilizzare questi oggetti salvati `PTTimedMetadata` durante la riproduzione, utilizzare il dizionario salvato da [Memorizzare gli oggetti con metadati temporizzati durante l&#39;invio](../../../tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-timed-metadata-store.md).

1. Estrai e aggiorna il tempo di riproduzione corrente da questa notifica e trova tutti gli oggetti `PTTimedMetadata` con orari di avvio che corrispondono al tempo di riproduzione corrente.

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

1. Svuotare periodicamente le istanze obsolete `PTTimedMetadata` dall&#39;elenco per evitare che la memoria cresca continuamente.
