---
description: Quando l'utente avanza o riavvolge rapidamente il supporto, si trova nella modalità di riproduzione con trucco. Per accedere alla modalità di riproduzione con trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
title: Implementazione di avanzamento rapido e riavvolgimento
exl-id: 21f9a3f6-1cae-4240-991d-c03a0e49adf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Implementazione di avanzamento rapido e riavvolgimento{#implement-fast-forward-and-rewind}

Quando l&#39;utente avanza o riavvolge rapidamente il supporto, si trova nella modalità di riproduzione con trucco. Per accedere alla modalità di riproduzione con trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

>[!IMPORTANT]
>
>* La modalità di riproduzione dei brani è supportata solo per contenuti MPEG Dash e HLS VOD.
>* La modalità di riproduzione dei brani non è supportata per gli annunci o i flussi live.
>* Quando si passa dal contenuto principale a un annuncio, il browser TVSDK lascia la modalità di riproduzione con trucco.
>


Per cambiare la velocità, è necessario impostare un valore.

1. Passare dalla modalità di riproduzione normale (1x) alla modalità di riproduzione con trazione impostando la frequenza su `MediaPlayer` a un valore consentito.

   * Il `MediaPlayerItem` classe definisce le velocità di riproduzione consentite.
   * Se la frequenza specificata non è consentita, il TVSDK del browser seleziona la frequenza consentita più vicina.

      La funzione di esempio seguente imposta la velocità:

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      La funzione di esempio seguente può essere utilizzata per eseguire una query sulle frequenze di riproduzione disponibili:

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. Facoltativamente, è possibile ascoltare gli eventi di variazione di tasso, che consentono di sapere quando è stata richiesta una modifica di tasso e quando si verifica effettivamente una modifica di tasso.

       Il browser TVSDK invia i seguenti eventi relativi alla riproduzione con trucco:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando `rate` il valore viene modificato in un valore diverso.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando la riproduzione riprende alla velocità selezionata.

      Il browser TVSDK invia entrambi questi eventi quando il lettore ritorna dalla modalità di riproduzione con trucco alla modalità di riproduzione normale.

## Elementi API per la modifica della velocità {#rate-change-API-elements}

Browser TVSDK include metodi, proprietà ed eventi per determinare i tassi validi, i tassi correnti, se è supportata la riproduzione con trucco e altre funzionalità correlate all&#39;avanzamento e al riavvolgimento rapido.

Utilizza i seguenti elementi API per modificare le percentuali di riproduzione:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - specifica tariffe valide.

   | Valore tariffa | Effetto sulla riproduzione |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più rapidamente del normale (ad esempio, 4 è 4 volte più veloce del normale) |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Passa alla modalità di riavvolgimento rapido |
   | 1.0 | Passa alla modalità di riproduzione normale (chiamata `play` equivale a impostare la proprietà rate su 1,0) |
   | 0.0 | Pause (chiamata `pause` equivale a impostare la proprietà rate su 0,0) |

## Limitazioni e comportamento per la riproduzione con trucco {#limitations-and-behavior-trick-play}

Ci sono alcune limitazioni e alcuni problemi nel modo in cui la modalità di riproduzione con trucco si comporta.

Di seguito è riportato un elenco delle limitazioni della modalità di riproduzione con trick:

* Se il flusso non contiene un adattamento per la riproduzione mediante trucco, il riavvolgimento rapido viene disattivato e la velocità di riproduzione massima per l&#39;avanzamento rapido è limitata a 8.
* Quando si utilizzano adattatori di riproduzione per fornire la modalità di riproduzione, la traccia audio viene disattivata.
* In modalità di riproduzione con trucco, il passaggio tra audio e tracce di sottotitoli è disattivato.
* Riproduci e pausa sono attivati.
* Alla ricerca, se la riproduzione è in modalità di riproduzione con trucco, la velocità di riproduzione è impostata su 1 e la riproduzione normale riprende.
* La logica ABR (Adaptive Bit Rate) è abilitata.

   Quando si utilizzano adattamenti normali, i profili sono limitati tra `ABRControlParameters.minBitRate` e `ABRControlParameters.maxBitRate`. Quando si utilizzano adattamenti per la riproduzione con trucco, i profili sono limitati tra `ABRControlParameters.minTrickPlayBitRate` e `ABRControlParameters.maxTrickPlayBitRate`.
