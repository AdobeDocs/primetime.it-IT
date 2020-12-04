---
description: Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.
seo-description: Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.
seo-title: Utilizzare i metadati temporizzati
title: Utilizzare i metadati temporizzati
uuid: 9bbdaefa-4ac5-4e08-92b4-15ebe5c46864
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# Usa metadati temporizzati{#use-timed-metadata}

Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.

Per utilizzare questi oggetti `PTTimedMetadata` salvati durante la riproduzione, utilizzare il dizionario salvato da [Memorizzare gli oggetti metadati temporizzati durante l&#39;invio](../../../tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-timed-metadata-store.md).

1. Estrarre e aggiornare il tempo di riproduzione corrente da questa notifica e individuare tutti gli oggetti `PTTimedMetadata` con orari di inizio che corrispondono al tempo di riproduzione corrente.

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

1. Svuotare periodicamente le istanze `PTTimedMetadata` stantate dall&#39;elenco per evitare la crescita continua della memoria.
