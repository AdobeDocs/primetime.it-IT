---
description: Il TVSDK informa il client del lettore sulla disponibilità della notifica AVAssetMediaCharacteristicsWithMediaSelectionOptions interna utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-description: Il TVSDK informa il client del lettore sulla disponibilità della notifica AVAssetMediaCharacteristicsWithMediaSelectionOptions interna utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-title: Esporre i sottotitoli
title: Esporre i sottotitoli
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Esporre i sottotitoli {#expose-subtitles}

Il TVSDK informa il client del lettore sulla disponibilità della notifica AVAssetMediaCharacteristicsWithMediaSelectionOptions interna utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.

È possibile accedere ai sottotitoli disponibili tramite la proprietà `PTMediaPlayerItem` `subtitlesOptions`.

Per esporre i sottotitoli:

1. Registra il client come listener per la notifica `PTMediaPlayerMediaSelectionOptionsAvailableNotification`.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando il cliente riceve questa notifica, i sottotitoli sono pronti in `PTMediaPlayerItem`.
1. Implementare il metodo `onMediaPlayerItemMediaSelectionOptionsAvailable` simile al seguente esempio:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Per informazioni sulle tracce audio alternative, consultate [Audio alternativo](../../alternate-audio/ios-3x-alternate-audio.md).