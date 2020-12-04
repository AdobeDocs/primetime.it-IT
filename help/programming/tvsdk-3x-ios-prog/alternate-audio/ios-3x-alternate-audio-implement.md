---
description: L'audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
seo-description: L'audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: 2915a74f-5ec3-457e-890d-5c79be39f37a
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Accedere a tracce audio alternative {#access-alternate-audio-tracks}

L&#39;audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendete che MediaPlayer sia almeno nello stato `PTMediaPlayerStatusReady`.
1. Ascoltare l&#39;evento:

   notifica `PTMediaPlayerItemMediaSelectionOptionsAvailable`: È disponibile l&#39;elenco iniziale delle tracce audio.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Ottenete le tracce audio disponibili dall&#39;istanza `PTMediaPlayerItem`.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Facoltativo) Presentare all’utente le tracce disponibili.
1. Impostate la traccia audio selezionata sull&#39;istanza `PTMediaPlayerItem`.
