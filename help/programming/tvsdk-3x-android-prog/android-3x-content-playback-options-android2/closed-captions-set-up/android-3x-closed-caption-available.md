---
description: Potete selezionare una traccia da un elenco di tracce di sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attivata. Alcuni brani potrebbero non essere disponibili inizialmente, quindi ascoltare l'evento che indica che sono diventati disponibili altri brani.
seo-description: Potete selezionare una traccia da un elenco di tracce di sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attivata. Alcuni brani potrebbero non essere disponibili inizialmente, quindi ascoltare l'evento che indica che sono diventati disponibili altri brani.
seo-title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
uuid: ee2bda5e-e398-4d09-bc5c-5a6adbf5f603
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Selezionare una traccia di didascalia corrente tra le tracce disponibili {#select-a-current-caption-track-from-among-available-tracks}

Potete selezionare una traccia da un elenco di tracce di sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attivata. Alcuni brani potrebbero non essere disponibili inizialmente, quindi ascoltare l&#39;evento che indica che sono diventati disponibili altri brani.

1. Attendete che il lettore multimediale sia almeno nello `PREPARED` stato.
1. Ascoltare i seguenti eventi:

   * `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZED`: È disponibile l’elenco iniziale di tracce di sottotitoli codificati.

1. Ottenete un elenco di tutte le tracce di sottotitoli codificati attualmente disponibili.

   Ad esempio:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Selezionate una traccia disponibile come traccia corrente.

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

1. Implementare un listener per l&#39;evento che indica che sono disponibili più tracce. Quando TVSDK invia l’evento, recuperate l’elenco corrente delle tracce disponibili.

   Recuperate l’elenco ogni volta che si verifica l’evento per essere certi di disporre sempre dell’elenco più recente.