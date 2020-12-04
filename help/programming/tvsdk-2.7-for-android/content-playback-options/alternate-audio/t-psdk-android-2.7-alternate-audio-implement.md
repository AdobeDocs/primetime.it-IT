---
description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: 9cec3a00-1416-497d-8d16-0ee429c8b575
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Accedere a tracce audio alternative {#access-alternate-audio-tracks}

L&#39;audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.

1. Attendere che lo stato `MediaPlayer` sia almeno uguale a `MediaPlayerStatus.PREPARED`.
1. Ascoltare l&#39;evento `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARED`.

   Questo passaggio indica che è disponibile l&#39;elenco iniziale di tracce audio.

1. Ottenete le tracce audio disponibili dall&#39;istanza `MediaPlayerItem`.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Facoltativo) Presentare all’utente le tracce disponibili.
1. Impostate la traccia audio selezionata sull&#39;istanza `MediaPlayerItem`.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

