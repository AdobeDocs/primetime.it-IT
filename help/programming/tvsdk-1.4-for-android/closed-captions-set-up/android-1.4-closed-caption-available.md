---
description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 53924aa8ba90555d58d15ee10fb14221c7dffaff
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---


# Selezionare una traccia di didascalia corrente tra le tracce disponibili{#select-a-current-caption-track-from-among-available-tracks}

Potete selezionare una traccia da un elenco di tracce di sottotitoli attualmente disponibili. Questa diventa la traccia corrente, che viene visualizzata quando la visibilità è attivata. Alcuni brani potrebbero non essere disponibili inizialmente, quindi ascoltare l&#39;evento che indica che sono diventati disponibili altri brani.

>[!TIP]
>
>I sottotitoli codificati sono sempre attivati. Vengono considerate presenti tutte le tracce predefinite dei sottotitoli. Le tracce predefinite (come CC1-CC4, CS1-CS6) sono enumerate in `ClosedCaptionsTrack.DefaultCCTypes`. All’inizio della riproduzione, TVSDK cerca l’attività su uno di questi canali. Se trova attività, imposta il metodo `isActive` per tale traccia e invia l&#39;evento `MediaPlayer.PlaybackEventListener.onUpdated`.

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implementare un listener per l&#39;evento che indica che sono disponibili più tracce. Quando TVSDK invia l’evento, recuperate l’elenco corrente delle tracce disponibili.

   Recuperate l’elenco ogni volta che si verifica l’evento per essere certi di disporre sempre dell’elenco più recente.
