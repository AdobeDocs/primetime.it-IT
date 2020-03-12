---
description: Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
seo-description: Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
seo-title: Implementazione rapida in avanti e indietro
title: Implementazione rapida in avanti e indietro
uuid: c1992757-d067-4c11-8d08-fec09099476f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Implementazione rapida in avanti e indietro{#implement-fast-forward-and-rewind}

Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

>[!IMPORTANT]
>
>* La modalità di riproduzione dei mattoni è supportata solo per i contenuti MPEG Dash e HLS VOD.
>* La modalità di riproduzione dei mattoni non è supportata per i flussi live o gli annunci.
>* Quando si passa dal contenuto principale a un annuncio, Browser TVSDK lascia la modalità di riproduzione ingannevole.
>



Per cambiare la velocità, è necessario impostare un valore.

1. Passa dalla modalità di riproduzione normale (1x) alla modalità di riproduzione ingannevole impostando la frequenza sulla modalità `MediaPlayer` a un valore consentito.

   * La `MediaPlayerItem` classe definisce le frequenze di riproduzione consentite.
   * Browser TVSDK seleziona la tariffa più vicina consentita se la frequenza specificata non è consentita.

      La seguente funzione di esempio imposta la frequenza:

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      La seguente funzione di esempio può essere utilizzata per eseguire una query sulle frequenze di riproduzione disponibili:

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. Facoltativamente, puoi ascoltare gli eventi relativi ai cambiamenti di tasso, che ti permettono di sapere quando hai richiesto un cambiamento di tasso e quando un cambiamento di tasso si verifica effettivamente.

       Browser TVSDK invia gli eventi seguenti relativi alla riproduzione a trucco:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando il `rate` valore cambia in un altro valore.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando la riproduzione riprende alla frequenza selezionata.

      Browser TVSDK invia entrambi questi eventi quando il lettore ritorna dalla modalità di riproduzione trucco alla modalità di riproduzione normale.

## Elementi API Rate-change {#rate-change-API-elements}

Il TVSDK del browser include metodi, proprietà ed eventi per determinare le percentuali valide, le frequenze correnti, se è supportata la riproduzione a circuito chiuso e altre funzionalità correlate a avanzamento rapido e riavvolgimento.

Utilizzate i seguenti elementi API per modificare le percentuali di riproduzione:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - specifica le tariffe valide.

   | Valore rate | Effetto sulla riproduzione |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più veloce del normale (ad esempio, 4 è 4 volte più veloce del normale) |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Passa alla modalità di riavvolgimento rapido |
   | 1.0 | Passa alla modalità di riproduzione normale (la chiamata `play` equivale a impostare la proprietà rate su 1.0) |
   | 0.0 | Pause (la chiamata `pause` è la stessa dell&#39;impostazione della proprietà rate su 0.0) |

## Limitazioni e comportamento per il trucco {#limitations-and-behavior-trick-play}

Ci sono alcuni limiti e alcuni problemi nel modo in cui la modalità di gioco trucco si comporta.

Di seguito è riportato un elenco delle limitazioni della modalità &quot;trucco&quot;:

* Se il flusso non contiene un adattamento di gioco trucco, il riavvolgimento veloce è disattivato, e la velocità massima di gioco per il avanzamento veloce è limitata a 8.
* Quando si utilizzano gli adattamenti di riproduzione trucco per fornire la modalità trucco, la traccia audio è disattivata.
* In modalità di riproduzione trucco, la commutazione di tracce audio e di sottotitoli codificati è disattivata.
* Riproduci e Pausa sono abilitati.
* Alla ricerca, se la riproduzione è in modalità di riproduzione a trucco, la frequenza di riproduzione è impostata su 1 e la riproduzione normale riprende.
* La logica ABR (Adaptive Bit Rate) è abilitata.

   Quando si utilizzano i normali adattamenti, i profili sono limitati tra `ABRControlParameters.minBitRate` e `ABRControlParameters.maxBitRate`. Quando si utilizzano gli adattamenti di riproduzione trucco, i profili sono limitati tra `ABRControlParameters.minTrickPlayBitRate` e `ABRControlParameters.maxTrickPlayBitRate`.