---
description: TVSDK fornisce API e codice di esempio per la gestione dei periodi di blackout.
seo-description: TVSDK fornisce API e codice di esempio per la gestione dei periodi di blackout.
seo-title: Implementare la gestione della blackout
title: Implementare la gestione della blackout
uuid: a447ff24-8386-4cae-878e-0859fb191de2
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Implementare la gestione della blackout {#implement-blackout-handling}

TVSDK fornisce API e codice di esempio per la gestione dei periodi di blackout.

Per implementare la gestione della blackout e fornire contenuto alternativo durante la blackout:

1. Configurate l&#39;app per iscrivervi ai tag blackout in un manifesto del flusso live.

   ```
   - (void) createMediaPlayer:(PTMediaPlayerItem *)item 
   { 
       [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:<INSERT-BLACKOUT-TAG>]]; 
       // For example:  
       // [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-OATCLS-SCTE35"]]; 
   }
   ```

1. Aggiungete un listener di notifica per `PTTimedMetadataChangedNotification`.

   ```
   - (void)addobservers 
   { 
       [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerSubscribedTagIdentified:)  
         name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
   }
   ```

1. Implementare un metodo listener per `PTTimedMetadata` gli oggetti in primo piano.

   Ad esempio:

   ```
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]  
         retain]; 
   
    if ([timedMetadata.name isEqualToString:<INSERT-BLACKOUT-TAG>]) 
       { 
        // handle tag. For example: store it in a dictionary keyed by time to be handled when  
        //   playback time = timedMetadata time. 
           NSNumber *timedMetadataStartTime =  
             [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
   
       [timedMetadata release]; 
   }
   ```

1. Gestione `TimedMetadata` degli oggetti con aggiornamenti costanti durante la riproduzione.

   ```
   - (void)onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       @synchronized(self) 
       { 
           CMTimeRange seekableRange = self.player.seekableRange; 
           if (CMTIMERANGE_IS_VALID(seekableRange)) 
           { 
               _currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
               if (isnan(_currentTime)) 
               { 
                   _currentTime = 0; 
               } 
               [self handleCollectionAtTime:_currentTime]; 
           } 
       } 
   }
   ```

1. Aggiungete il `PTTimedMetadata` gestore per passare al contenuto alternativo e tornare al contenuto principale come indicato dall&#39; `PTTimedMetadata` oggetto e il relativo tempo di riproduzione.

   ```
   - (void)handleCollectionAtTime:(int)currentTime 
   { 
       NSArray *allKeys = nil; 
       NSMutableArray * timedMetadatasToDelete = [[[NSMutableArray alloc]init]autorelease]; 
   
       if (!_inBlackout && timedMetadataCollection) 
       { 
           allKeys = [timedMetadataCollection allKeys]; 
           int count = [allKeys count]; 
           for (int i=count-1; i>-1; i--) 
           { 
               NSNumber *currTimedMetadataTime = allKeys[i]; 
               PTTimedMetadata *currTimedMetadata =  
                 [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
   
               if (currentTime == [currTimedMetadataTime integerValue] &&  
                                  currTimedMetadata.name == <INSERT-BLACKOUT-TAG> &&  
                                  [self isBlackoutStart: currTimedMetadata]) 
               { 
                                   PTAdMetadata *newItemAdMetadata =  
                                     [self createAlternateMediaMetadata];            
   
               // 1. Turn off preroll on the alternate media item. 
                   newItemAdMetadata.enableLivePreroll = NO; 
   
                               PTMediaPlayerItem *newItem =  
                                 [[PTMediaPlayerItem alloc]initWithUrl: 
                                   <INSERT-ALTERNATE-STREAM-URL mediaId:<INSERT-ALTERNATE-STREAM- 
                                    MEDIA-ID> metadata:newItemAdMetadata];
   
              // 2. Register the current (original playback item) in background. 
                   [self.player registerCurrentItemAsBackgroundItem]; 
   
              // 3. Replace the current playback item with the alternate stream. 
                    [self.player replaceCurrentItemWithPlayerItem:newItem]; 
   
              // 4. Reset observers. 
                   [self removeObservers]; 
                   [self addobservers]; 
   
              // 5. Register listener on the subscribed tags in background item. 
                   [[NSNotificationCenter defaultCenter] addObserver:self  
                      selector:@selector(onSubscribedTagInBackground:)  
                       name:PTTimedMetadataChangedInBackgroundNotification  
                         object:self.player.currentItem]; 
   
              // 6. Register listener on the error in background item. 
                            [[NSNotificationCenter defaultCenter]  
                               addObserver:self selector:@selector(onBackgroundManifestError:)  
                               name:PTBackgroundManifestErrorNotification   
                                 object:self.player.currentItem]; 
   
              // 7. Resume playback 
                        [self.player play]; 
   
                       // 8. Set boolean to true to handle blackout end. 
                     _inBlackout = YES; 
                     break; 
               } 
           } 
       } 
       else if (_inBlackout && backgroundTimedMetadataCollection) 
       { 
           allKeys = [backgroundTimedMetadataCollection allKeys]; 
           int count = [allKeys count]; 
           for (int i=count-1; i>-1; i--) 
           { 
               NSNumber *currTimedMetadataTime = allKeys[i]; 
               PTTimedMetadata *currTimedMetadata =  
                 [backgroundTimedMetadataCollection objectForKey:allKeys[i]]; 
   
               if (currentTime == ([currTimedMetadataTime integerValue] &&  
                 currTimedMetadata.name == <INSERT-BLACKOUT-TAG>  &&  
                 [self isBlackoutEnd:currTimedMetadata] ) 
               {      
                                  // 1. Come out of blackout. Unregister background item. 
                              [self.player unregisterCurrenBackgroundItem]; 
   
                       PTMetadata *metadata = [self createMetadata]; 
                       PTAdMetadata *adMetadata =  
                         (PTAdMetadata *)[currMetadata metadataForKey:PTAdResolvingMetadataKey]; 
                             adMetadata.enableLivePreroll = NO; 
   
                               PTMediaPlayerItem *item =  
                                 [[[PTMediaPlayerItem alloc] initWithUrl:<INSERT-ORIGINAL-URL>  
                                   mediaId:<INSERT-ORIGINAL-MEDIAID> metadata:metadata autorelease]; 
   
                                   // 2. Switch back to original item. 
                       [self.player replaceCurrentItemWithPlayerItem:item]; 
                       self.player.autoPlay = YES; 
                       [self removeObservers]; 
   
                       // 3. Remove background item listener. 
                       [[NSNotificationCenter defaultCenter] removeObserver:self  
                          name:PTTimedMetadataChangedInBackgroundNotification  
                       object:self.player.currentItem]; 
   
                                  [[NSNotificationCenter defaultCenter] removeObserver:self  
                                     name:PTBackgroundManifestErrorNotification 
                       object:self.player.currentItem]; 
                       [self addobservers]; 
                       [self.player play]; 
   
                               // 4. Update boolean to correctly maintain the current state. 
                       _inBlackout = NO; 
                       break; 
               } 
           } 
       } 
   }
   ```

1. Implementare un metodo listener per `PTTimedMetadata` gli oggetti in background.

   ```
   - (void)onSubscribedTagInBackground:(NSNotification *)notification 
   { 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *) 
         [userInfo objectForKey:PTTimedMetadataKey] retain]; 
   
       if ([timedMetadata.name isEqualToString:<INSERT-BLACKOUT-TAG>]) 
       { 
           NSNumber *timedMetadataStartTime =  
             [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [backgroundTimedMetadataCollection  
              setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
   
       [timedMetadata release]; 
   }
   ```

1. Implementare un metodo listener per gli errori in background.

   ```
   - (void) onBackgroundManifestError:(NSNotification *)notification 
   { 
       NSLog (@"onBackgroundManifestError"); 
   }
   ```

1. Se l’intervallo di blackout è sul DVR nel flusso di riproduzione, aggiornate gli intervalli non ricercabili.

   ```
   // This sample assumes that blackoutStartTimedMetadata is the PTTimedMetadata  
   // object that indicated "blackout start", and assuming blackoutEndTimedMetadata is the  
   // PTTimedMetadataObject that indicated "blackout end". Since in this case they are both  
   // in DVR, both are notified to the application before playback starts. This is the right  
   // time for the application to set this range in DVR as non-seekable range. 
   
   CMTime ignoreRangeStart = blackoutStartTimedMetadata.time; 
   CMTime ignoreRangeDuration = CMTimeMakeWithSeconds(CMTimeMakeWithSeconds  
     (CMTimeGetSeconds(blackoutEndTimedMetadata.time) -   
        CMTimeGetSeconds(blackoutStartTimedMetadata.time)),  
          blackoutEndTimedMetadata.time.timescale); 
   
   CMTimeRange ignoreRange = CMTimeRangeMake(ignoreRangeStart, ignoreRangeDuration); 
   NSArray *ignoreRangeArray = [NSArray arrayWithObject:[NSValue valueWithCMTimeRange:ignoreRange]]; 
   PTBlackoutMetadata *blackoutMetadata =  
     [[PTBlackoutMetadata alloc]initWithNonSeekableRanges:ignoreRangeArray]; 
   PTMetadata *currMetadata = self.item.metadata; 
   
   if (currMetadata) 
   { 
       [currMetadata setMetadata:blackoutMetadata forKey:PTBlackoutMetadataKey] 
   }
   ```
