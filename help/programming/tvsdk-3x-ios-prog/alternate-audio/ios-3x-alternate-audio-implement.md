---
description: L'audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
exl-id: c95e2bae-fcf3-4ae2-be11-fb3191b380f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Accedere a tracce audio alternative {#access-alternate-audio-tracks}

L&#39;audio con associazione tardiva utilizza PTMediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendere che MediaPlayer sia incluso almeno nel `PTMediaPlayerStatusReady` stato.
1. Ascolta questo evento:

   notifica `PTMediaPlayerItemMediaSelectionOptionsAvailable`: è disponibile l’elenco iniziale delle tracce audio.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self 
        selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:) 
        name:PTMediaPlayerItemMediaSelectionOptionsAvailable  
        object:self.player];
   ```

1. Ottieni le tracce audio disponibili da `PTMediaPlayerItem` dell&#39;istanza.

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

1. (Facoltativo) Presenta all&#39;utente i brani disponibili.
1. Imposta la traccia audio selezionata su `PTMediaPlayerItem` dell&#39;istanza.
