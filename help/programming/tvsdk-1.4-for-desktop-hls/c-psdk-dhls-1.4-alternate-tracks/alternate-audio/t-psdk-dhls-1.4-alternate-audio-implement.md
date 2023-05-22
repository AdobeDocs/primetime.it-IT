---
description: L'audio di associazione tardiva utilizza MediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
exl-id: 08158b3b-1ed2-4f86-a710-2b128bb28ed0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Accedere a tracce audio alternative{#access-alternate-audio-tracks}

L&#39;audio di associazione tardiva utilizza MediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendi `MediaPlayer` essere almeno nello stato PREPARATO.
1. Ascolta questi eventi:

   * `MediaPlayerItemEvent.ITEM_CREATED`: è disponibile l’elenco iniziale delle tracce audio.
   * `MediaPlayerItemEvent.AUDIO_UPDATED`: tracce audio modificate durante la riproduzione

1. Ottieni le tracce audio disponibili da `MediaPlayerItem` dell&#39;istanza.
1. (Facoltativo) Presenta all&#39;utente i brani disponibili.
1. Imposta la traccia audio selezionata su `MediaPlayerItem` dell&#39;istanza.
