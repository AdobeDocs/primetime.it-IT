---
description: È possibile selezionare un brano da un elenco di brani con sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attiva. Alcuni brani potrebbero non essere inizialmente disponibili, quindi ascolta l’evento che indica che sono stati resi disponibili altri brani.
title: Seleziona una traccia di didascalia corrente tra le tracce disponibili
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Seleziona una traccia di didascalia corrente tra le tracce disponibili {#select-a-current-caption-track-from-among-available-tracks}

È possibile selezionare un brano da un elenco di brani con sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attiva. Alcuni brani potrebbero non essere inizialmente disponibili, quindi ascolta l’evento che indica che sono stati resi disponibili altri brani.

1. Attendi che il lettore multimediale si trovi almeno nel `PREPARED` stato.
1. Ascolta questi eventi:

   * `MediaPlayerEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZED`: è disponibile l’elenco iniziale dei brani con sottotitoli.

1. Ottieni un elenco di tutte le tracce di sottotitoli attualmente disponibili.

   Ad esempio:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Selezionate un brano disponibile come brano corrente.

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

1. Implementa un listener per l’evento che indica che sono disponibili più tracce. Quando TVSDK invia l’evento, recupera l’elenco corrente dei brani disponibili.

   Recupera l’elenco ogni volta che si verifica l’evento, per assicurarti di disporre sempre dell’elenco più recente.
