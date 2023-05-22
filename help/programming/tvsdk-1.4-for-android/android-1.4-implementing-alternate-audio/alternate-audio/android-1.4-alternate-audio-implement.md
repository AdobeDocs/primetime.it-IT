---
description: L'audio di associazione tardiva utilizza MediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
exl-id: d357bcc9-2996-42f0-a733-482f59e938ac
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio di associazione tardiva utilizza MediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendere che MediaPlayer sia almeno nello stato READY.
1. Ascolta questo evento:

   `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: è disponibile l’elenco iniziale delle tracce audio.

1. Ottieni le tracce audio disponibili da `MediaPlayerItem` dell&#39;istanza.

   `mediaPlayerItem.getAudioTracks()` 1. (Facoltativo) Presenta all&#39;utente i brani disponibili.
1. Imposta la traccia audio selezionata su `MediaPlayerItem` dell&#39;istanza.

   `mediaPlayerItem.selectAudioTrack(audioTrack)`
