---
description: L'audio in ritardo utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio in ritardo utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendi che MediaPlayer sia almeno nello stato `PTMediaPlayerStatusReady` .
1. Ascolta questo evento:

   notifica `PTMediaPlayerItemMediaSelectionOptionsAvailable`: È disponibile l&#39;elenco iniziale delle tracce audio.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Ottieni le tracce audio disponibili dall&#39;istanza `PTMediaPlayerItem`.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Facoltativo) Presentare all&#39;utente le tracce disponibili.
1. Imposta la traccia audio selezionata sull&#39;istanza `PTMediaPlayerItem`.
