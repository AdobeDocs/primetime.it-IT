---
description: TVSDK notifica al client del lettore la disponibilità di AVAsset interno disponibileMediaCharacteristicsWithMediaSelectionOptions utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Esposizione sottotitoli
exl-id: dc726a5b-2eab-4ebd-8773-7396bf818205
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Esposizione sottotitoli {#expose-subtitles}

TVSDK notifica al client del lettore la disponibilità di AVAsset interno disponibileMediaCharacteristicsWithMediaSelectionOptions utilizzando la notifica PTMediaPlayerMediaSelectionOptionsAvailableNotification.

È possibile accedere ai sottotitoli disponibili tramite `PTMediaPlayerItem` proprietà `subtitlesOptions`.

Per esporre i sottotitoli:

1. Registrare il client come listener per `PTMediaPlayerMediaSelectionOptionsAvailableNotification` notifica.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Quando il client riceve questa notifica, i sottotitoli sono pronti nel `PTMediaPlayerItem`.
1. Implementare `onMediaPlayerItemMediaSelectionOptionsAvailable` metodo simile al seguente esempio:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Per informazioni sulle tracce audio alternative, consultate  [Audio alternativo](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
