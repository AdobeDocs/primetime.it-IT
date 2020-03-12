---
description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: 09aa00e9-0cbf-4f5b-9652-ce514f6e2f38
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

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
