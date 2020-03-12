---
description: L'audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
seo-description: L'audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: 77e39633-bf17-4a06-a2a1-93fdaadedd17
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendete che MediaPlayer sia almeno nello `PTMediaPlayerStatusReady` stato.
1. Ascoltare l&#39;evento:

   notifica `PTMediaPlayerItemMediaSelectionOptionsAvailable`: È disponibile l&#39;elenco iniziale delle tracce audio.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Ottenete le tracce audio disponibili dall’ `PTMediaPlayerItem` istanza.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Facoltativo) Presentare all’utente le tracce disponibili.
1. Impostate la traccia audio selezionata sull’ `PTMediaPlayerItem` istanza.
