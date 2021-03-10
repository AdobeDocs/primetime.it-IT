---
description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Accedere a tracce audio alternative {#access-alternate-audio-tracks}

L&#39;audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.

1. Attendi che lo stato `MediaPlayer` sia almeno lo stato `MediaPlayerStatus.PREPARED`.
1. Ascolta l’evento `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARED`.

   Questo passaggio indica che è disponibile l&#39;elenco iniziale delle tracce audio.

1. Ottieni le tracce audio disponibili dall&#39;istanza `MediaPlayerItem`.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Facoltativo) Presentare all&#39;utente le tracce disponibili.
1. Imposta la traccia audio selezionata sull&#39;istanza `MediaPlayerItem`.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```

