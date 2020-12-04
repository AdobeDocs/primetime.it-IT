---
description: L'audio con binding ritardato utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-description: L'audio con binding ritardato utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: c7060022-29ec-43c1-811b-41cca5f5356c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio con binding ritardato utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.

1. Attendete che MediaPlayer sia almeno nello stato PREPARATO.
1. Ascoltare l&#39;evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: È disponibile l&#39;elenco iniziale delle tracce audio.

1. Ottenete le tracce audio disponibili dall&#39;istanza `MediaPlayerItem`.

   `mediaPlayerItem.getAudioTracks()` 1. (Facoltativo) Presentare all’utente le tracce disponibili.
1. Impostate la traccia audio selezionata sull&#39;istanza `MediaPlayerItem`.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`