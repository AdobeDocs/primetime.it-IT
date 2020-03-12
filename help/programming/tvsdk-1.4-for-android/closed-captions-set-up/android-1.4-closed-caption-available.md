---
description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Selezionare una traccia di didascalia corrente tra le tracce disponibili{#select-a-current-caption-track-from-among-available-tracks}

Potete selezionare una traccia da un elenco di tracce di sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attivata. Alcuni brani potrebbero non essere disponibili inizialmente, quindi ascoltare l&#39;evento che indica che sono diventati disponibili altri brani.

>[!TIP]
>
>I sottotitoli codificati sono sempre attivati. Vengono considerate presenti tutte le tracce predefinite dei sottotitoli. Le tracce predefinite (come CC1-CC4, CS1-CS6) sono enumerate in `ClosedCaptionsTrack.DefaultCCTypes`. All’inizio della riproduzione, TVSDK cerca l’attività su uno di questi canali. Se trova l&#39;attività, imposta il `isActive` metodo per tale tracciamento e invia l&#39; `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Attendete che il lettore multimediale sia almeno nello stato PREPARATO.
1. Ascoltare i seguenti eventi:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: È disponibile l&#39;elenco iniziale di tracce di sottotitoli

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

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

