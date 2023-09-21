---
description: Quando l'utente avanza o riavvolge rapidamente il supporto, si trova nella modalità di riproduzione con trucco. Per accedere alla modalità di riproduzione con trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
title: Implementazione di avanzamento rapido e riavvolgimento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Panoramica {#implement-fast-forward-and-rewind}

Quando l&#39;utente avanza o riavvolge rapidamente il supporto, si trova nella modalità di riproduzione con trucco. Per accedere alla modalità di riproduzione con trucco, impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

Per cambiare la velocità, è necessario impostare un valore.

1. Passare dalla modalità di riproduzione normale (1x) alla modalità di riproduzione con trazione impostando la frequenza su `MediaPlayer` a un valore consentito.

       Tenere presenti le seguenti informazioni:
   
   * Il `MediaPlayerItem` classe definisce le velocità di riproduzione consentite.
   * Se la tariffa specificata non è consentita, TVSDK seleziona la tariffa consentita più vicina.

     L’esempio che segue imposta la velocità di riproduzione interna del lettore sulla velocità richiesta:

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

1. Facoltativamente, è possibile ascoltare gli eventi di modifica della tariffa, che avvisa quando è stata richiesta una modifica della tariffa e quando si verifica effettivamente la modifica della tariffa.

TVSDK invia i seguenti eventi relativi alla riproduzione con trucco:

* `MediaPlayerEvent.RATE_SELECTED`, quando `rate` il valore viene modificato in un valore diverso.

* `MediaPlayerEvent.RATE_PLAYING`, quando la riproduzione riprende alla velocità selezionata.

  TVSDK invia questi eventi quando il lettore ritorna dalla modalità di riproduzione con trucco alla modalità di riproduzione normale.
