---
description: L'audio in ritardo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio in ritardo utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.

1. Attendere che MediaPlayer sia almeno nello stato PREPARATO.
1. Ascolta questo evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: È disponibile l&#39;elenco iniziale delle tracce audio.

1. Ottieni le tracce audio disponibili dall&#39;istanza `MediaPlayerItem`.

   `mediaPlayerItem.getAudioTracks()` 1. (Facoltativo) Presentare all&#39;utente le tracce disponibili.
1. Imposta la traccia audio selezionata sull&#39;istanza `MediaPlayerItem`.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`