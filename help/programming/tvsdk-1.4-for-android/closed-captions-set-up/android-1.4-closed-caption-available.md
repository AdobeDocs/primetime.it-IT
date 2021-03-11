---
description: I sottotitoli codificati visualizzano la parte audio di un video sotto forma di testo sullo schermo quando l’audio non è udibile o l’utente non è udito.
title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 1%

---


# Selezionare una traccia di didascalia corrente tra le tracce disponibili{#select-a-current-caption-track-from-among-available-tracks}

È possibile selezionare una traccia da un elenco di tracce a didascalia chiusa attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attiva. Alcune tracce potrebbero non essere disponibili all&#39;inizio, quindi ascolta l&#39;evento che indica che sono state rese disponibili altre tracce.

>[!TIP]
>
>I sottotitoli codificati sono sempre abilitati. Tutte le tracce di didascalia chiusa predefinite sono considerate presenti. Le tracce predefinite (come CC1-CC4, CS1-CS6) sono enumerate in `ClosedCaptionsTrack.DefaultCCTypes`. Quando la riproduzione inizia, TVSDK cerca l’attività su uno di questi canali. Se trova l&#39;attività, imposta il metodo `isActive` per quel brano e invia l&#39;evento `MediaPlayer.PlaybackEventListener.onUpdated` .

1. Attendi che il lettore multimediale sia almeno nello stato PREPARATO.
1. Ascolta questi eventi:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: È disponibile l’elenco iniziale di tracce a didascalia chiusa

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implementa un listener per l&#39;evento che indica che sono disponibili più tracce. Quando TVSDK invia l’evento, recupera l’elenco corrente delle tracce disponibili.

   Recupera l’elenco ogni volta che si verifica l’evento per assicurarti di disporre sempre dell’elenco più aggiornato.
