---
description: L'audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.
title: Accedere a tracce audio alternative
exl-id: e5f5b943-4886-4884-80d2-225b5c7e3aed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Accedere a tracce audio alternative {#access-alternate-audio-tracks}

L&#39;audio alternativo utilizza MediaPlayer per riprodurre un video specificato in una playlist HLS M3U8 e che può contenere diversi flussi audio alternativi.

1. Attendi `MediaPlayer` essere almeno nel `MediaPlayerStatus.PREPARED` stato.
1. Ascolta la `MediaPlayerEvent.STATUS_CHANGED` evento con stato `MediaPlayerStatus.PREPARED`.

   Questo passaggio indica che è disponibile l&#39;elenco iniziale delle tracce audio.

1. Ottieni le tracce audio disponibili da `MediaPlayerItem` dell&#39;istanza.

   ```java
   mediaPlayerItem.getAudioTracks()
   ```

1. (Facoltativo) Presenta all&#39;utente i brani disponibili.
1. Imposta la traccia audio selezionata su `MediaPlayerItem` dell&#39;istanza.

   ```java
   mediaPlayerItem.selectAudioTrack(audioTrack)
   ```
