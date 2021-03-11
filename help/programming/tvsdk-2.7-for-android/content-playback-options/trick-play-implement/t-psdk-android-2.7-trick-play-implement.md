---
description: Quando gli utenti avanzano velocemente o riavvolgono velocemente i contenuti multimediali, si trovano in modalità di riproduzione a trucco. Per accedere alla modalità di riproduzione a trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
title: Implementazione rapida in avanti e in riavvolgimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Panoramica {#implement-fast-forward-and-rewind-overview}

Quando gli utenti avanzano velocemente o riavvolgono velocemente i contenuti multimediali, si trovano in modalità di riproduzione a trucco. Per accedere alla modalità di riproduzione a trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

Per cambiare la velocità, è necessario impostare un valore.

1. Passa dalla modalità di riproduzione normale (1x) alla modalità di riproduzione con trucco impostando la velocità su `MediaPlayer` su un valore consentito.

       Ricorda le seguenti informazioni:
   
   * La classe `MediaPlayerItem` definisce le velocità di riproduzione consentite.
   * TVSDK seleziona la velocità consentita più vicina se la velocità specificata non è consentita.

      L&#39;esempio seguente imposta la velocità di riproduzione interna del lettore sulla velocità richiesta:

      ```
      import com.adobe.mediacore.MediaPlayer; 
      import com.adobe.mediacore.MediaPlayerItem; 
      import com.adobe.mediacore.MediaPlayerException; 
      import java.util.List; 
      import java.lang.Float; 
      
      private boolean setPlaybackRate(MediaPlayer player, float rate)  
        throws MediaPlayerException { 
          // Get list of playback rates that the media player supports 
          MediaPlayerItem item = player.getCurrentItem(); 
          if (item == null) return false; 
          List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
      
          // Return false if requested rate is not supported 
          if (availableRates.indexOf(rate) == -1) return false; 
      
          // Otherwise set the playback rate to the requested rate  
          // (this can throw MediaPlayerException) 
          player.setRate(rate); 
          return true; 
      }
      ```

1. Facoltativamente, puoi ascoltare gli eventi di variazione del tasso, che ti avvisa quando hai richiesto una variazione del tasso e quando la variazione del tasso si verifica effettivamente.

       TVSDK invia i seguenti eventi relativi al gioco a tre:
   
   * `MediaPlayerEvent.RATE_SELECTED`, quando il  `rate` valore cambia in un valore diverso.

   * `MediaPlayerEvent.RATE_PLAYING`, quando la riproduzione riprende alla velocità selezionata.

      TVSDK invia questi eventi quando il lettore ritorna dalla modalità di riproduzione a trucco alla modalità di riproduzione normale.

