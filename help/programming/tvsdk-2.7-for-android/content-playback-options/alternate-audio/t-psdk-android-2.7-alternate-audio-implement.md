---
description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Accedere a tracce audio alternative {#access-alternate-audio-tracks}

L&#39;audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.

1. Aspettate che `MediaPlayer` lo stato sia almeno `MediaPlayerStatus.PREPARED` .
1. Ascoltare l’ `MediaPlayerEvent.STATUS_CHANGED` evento con lo stato `MediaPlayerStatus.PREPARED`.

   Questo passaggio indica che è disponibile l&#39;elenco iniziale di tracce audio.

1. Ottenete le tracce audio disponibili dall’ `MediaPlayerItem` istanza.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Facoltativo) Presentare all’utente le tracce disponibili.
1. Impostate la traccia audio selezionata sull’ `MediaPlayerItem` istanza.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

