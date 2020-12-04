---
description: Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
seo-description: Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
seo-title: Implementazione rapida in avanti e indietro
title: Implementazione rapida in avanti e indietro
uuid: d54c8c61-887f-4362-9085-e443859854b9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Panoramica {#implement-fast-forward-and-rewind}

Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

Per cambiare la velocità, è necessario impostare un valore.

1. Passa dalla modalità di riproduzione normale (1x) alla modalità di riproduzione ingannevole impostando la velocità su `MediaPlayer` su un valore consentito.

       Ricorda le seguenti informazioni:
   
   * La classe `MediaPlayerItem` definisce le frequenze di riproduzione consentite.
   * TVSDK seleziona la tariffa più vicina consentita se la frequenza specificata non è consentita.

      L&#39;esempio seguente imposta la frequenza di riproduzione interna del lettore sulla frequenza richiesta:

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

1. Facoltativamente, puoi ascoltare gli eventi relativi ai cambiamenti di tasso, che ti avvisano quando hai richiesto una variazione di tasso e quando la variazione di tasso si verifica effettivamente.

TVSDK invia gli eventi seguenti relativi al trucco:

* `MediaPlayerEvent.RATE_SELECTED`, quando il  `rate` valore cambia in un altro valore.

* `MediaPlayerEvent.RATE_PLAYING`, quando la riproduzione riprende alla velocità selezionata.

   TVSDK invia questi eventi quando il lettore ritorna dalla modalità di riproduzione a quella normale.