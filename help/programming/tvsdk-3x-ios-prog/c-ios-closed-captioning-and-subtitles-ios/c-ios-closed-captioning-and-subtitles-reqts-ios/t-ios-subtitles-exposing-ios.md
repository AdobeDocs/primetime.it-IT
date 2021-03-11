---
description: Il TVSDK notifica al client del lettore la disponibilità della notifica availableMediaFeaturesWithMediaSelectionOptions interna di AVAsset utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Esporre i sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Esporre i sottotitoli {#expose-subtitles}

Il TVSDK notifica al client del lettore la disponibilità della notifica availableMediaFeaturesWithMediaSelectionOptions interna di AVAsset utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.

Puoi accedere ai sottotitoli disponibili tramite l’ `PTMediaPlayerItem` della proprietà `subtitlesOptions` .

Per esporre i sottotitoli:

1. Registra il client come listener per la notifica `PTMediaPlayerMediaSelectionOptionsAvailableNotification`.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando il cliente riceve questa notifica, i sottotitoli sono pronti in `PTMediaPlayerItem`.
1. Implementa il metodo `onMediaPlayerItemMediaSelectionOptionsAvailable` simile al seguente esempio:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Per informazioni sulle tracce audio alternative, vedere [Audio alternativo](../../alternate-audio/ios-3x-alternate-audio.md).