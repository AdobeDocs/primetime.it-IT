---
description: I sottotitoli codificati visualizzano la porzione audio di un video come testo sullo schermo quando l'audio non è udibile o lo spettatore è ipoudente.
title: Seleziona una traccia di didascalia corrente tra le tracce disponibili
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Seleziona una traccia di didascalia corrente tra le tracce disponibili{#select-a-current-caption-track-from-among-available-tracks}

È possibile selezionare un brano da un elenco di brani con sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attiva. Alcuni brani potrebbero non essere inizialmente disponibili, quindi ascolta l’evento che indica che sono stati resi disponibili altri brani.

>[!TIP]
>
>I sottotitoli codificati sono sempre abilitati. Tutte le tracce sottotitoli predefinite sono considerate presenti. I brani predefiniti (come CC1-CC4, CS1-CS6) sono elencati in `ClosedCaptionsTrack.DefaultCCTypes`. Quando inizia la riproduzione, TVSDK cerca l’attività su uno qualsiasi di questi canali. Se trova attività, imposta `isActive` metodo per tale tracciamento e invia `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Attendere che il lettore multimediale sia almeno nello stato PREPARATO.
1. Ascolta questi eventi:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: è disponibile l’elenco iniziale dei brani con sottotitoli

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implementa un listener per l’evento che indica che sono disponibili più tracce. Quando TVSDK invia l’evento, recupera l’elenco corrente dei brani disponibili.

   Recupera l’elenco ogni volta che si verifica l’evento, per assicurarti di disporre sempre dell’elenco più recente.
