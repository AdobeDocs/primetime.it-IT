---
description: L'audio con binding ritardato utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-description: L'audio con binding ritardato utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.
seo-title: Accedere a tracce audio alternative
title: Accedere a tracce audio alternative
uuid: 136b4f1b-e56f-4a8a-a961-05193434558c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio con binding ritardato utilizza MediaPlayer per riprodurre un video specificato in una playlist M3U8 HLS e che può contenere diversi flussi audio alternativi.

1. Attendete che lo stato `MediaPlayer` sia almeno PREPARATO.
1. Ascoltare i seguenti eventi:

   * `MediaPlayerItemEvent.ITEM_CREATED`: È disponibile l&#39;elenco iniziale delle tracce audio.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: Tracce audio modificate durante la riproduzione

1. Ottenete le tracce audio disponibili dall’ `MediaPlayerItem` istanza.
1. (Facoltativo) Presentare all’utente le tracce disponibili.
1. Impostate la traccia audio selezionata sull’ `MediaPlayerItem` istanza.
