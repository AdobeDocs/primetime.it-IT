---
description: È possibile selezionare una traccia da un elenco di tracce a didascalia chiusa attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attiva. Alcune tracce potrebbero non essere disponibili all'inizio, quindi ascolta l'evento che indica che sono state rese disponibili altre tracce.
title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---


# Selezionare una traccia di didascalia corrente tra le tracce disponibili {#select-a-current-caption-track-from-among-available-tracks}

È possibile selezionare una traccia da un elenco di tracce a didascalia chiusa attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attiva. Alcune tracce potrebbero non essere disponibili all&#39;inizio, quindi ascolta l&#39;evento che indica che sono state rese disponibili altre tracce.

1. Attendi che il lettore multimediale sia almeno nello stato `PREPARED`.
1. Ascolta questi eventi:

   * `MediaPlayerEvent.STATUS_CHANGED` con stato  `MediaPlayerStatus.INITIALIZED`: È disponibile l’elenco iniziale delle tracce di sottotitoli.

1. Ottenere un elenco di tutti i brani a didascalia chiusa attualmente disponibili.

   Ad esempio:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Seleziona una traccia disponibile come traccia corrente.

   Ad esempio:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implementa un listener per l&#39;evento che indica che sono disponibili più tracce. Quando TVSDK invia l’evento, recupera l’elenco corrente delle tracce disponibili.

   Recupera l’elenco ogni volta che si verifica l’evento per assicurarti di disporre sempre dell’elenco più aggiornato.