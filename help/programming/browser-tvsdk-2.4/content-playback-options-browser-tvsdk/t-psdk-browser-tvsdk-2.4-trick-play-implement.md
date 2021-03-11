---
description: Quando gli utenti avanzano velocemente o riavvolgono velocemente i contenuti multimediali, si trovano in modalità di riproduzione a trucco. Per accedere alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
title: Implementazione rapida in avanti e in riavvolgimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# Implementa avanzamento rapido e riavvolgimento{#implement-fast-forward-and-rewind}

Quando gli utenti avanzano velocemente o riavvolgono velocemente i contenuti multimediali, si trovano in modalità di riproduzione a trucco. Per accedere alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

>[!IMPORTANT]
>
>* La modalità di riproduzione a mattoni è supportata solo per i contenuti MPEG Dash e HLS VOD.
>* La modalità di riproduzione dei mattoni non è supportata per i flussi live o gli annunci.
>* Quando si passa dal contenuto principale a un annuncio, Browser TVSDK lascia la modalità di riproduzione a trucco.

>



Per cambiare la velocità, è necessario impostare un valore.

1. Passa dalla modalità di riproduzione normale (1x) alla modalità di riproduzione con trucco impostando la velocità su `MediaPlayer` su un valore consentito.

   * La classe `MediaPlayerItem` definisce le velocità di riproduzione consentite.
   * Il browser TVSDK seleziona la frequenza più vicina consentita se la frequenza specificata non è consentita.

      La funzione di esempio seguente imposta la frequenza:

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      La seguente funzione di esempio può essere utilizzata per eseguire una query sulle percentuali di riproduzione disponibili:

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. Facoltativamente, puoi ascoltare gli eventi di cambio di tasso, che ti permettono di sapere quando hai richiesto un cambiamento di tasso e quando un cambiamento di tasso si verifica effettivamente.

       Il browser TVSDK invia i seguenti eventi relativi alla riproduzione a trucco:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando il  `rate` valore cambia in un valore diverso.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando la riproduzione riprende alla velocità selezionata.

      Il browser TVSDK invia entrambi questi eventi quando il lettore ritorna dalla modalità di gioco-trucco alla modalità di riproduzione normale.

## Elementi API di modifica della velocità {#rate-change-API-elements}

Il TVSDK del browser include metodi, proprietà ed eventi per determinare le percentuali valide, le percentuali correnti, se è supportata la riproduzione di trucco e altre funzionalità relative alla riavvolgimento e avanzamento rapido.

Utilizza i seguenti elementi API per modificare le percentuali di riproduzione:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - specifica le percentuali valide.

   | Valore rate | Effetto sulla riproduzione |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più rapidamente del normale (ad esempio, 4 è 4 volte più veloce del normale) |
   | -2,0, -4,0, -8,0, -16,0, -32,0, -64,0 | Passa alla modalità di riavvolgimento rapido |
   | 1,0 | Passa alla modalità di riproduzione normale (chiamare `play` equivale a impostare la proprietà rate su 1.0) |
   | 0,0 | Sospensioni (la chiamata di `pause` equivale all&#39;impostazione della proprietà rate su 0.0) |

## Limitazioni e comportamento per il gioco a tre {#limitations-and-behavior-trick-play}

Ci sono alcune limitazioni e alcuni problemi nel modo in cui si comporta la modalità di gioco trucco.

Di seguito è riportato un elenco delle limitazioni della modalità di gioco-trucco:

* Se il flusso non contiene un adattamento di gioco a trucco, il riavvolgimento veloce è disabilitato e il tasso di gioco massimo per avanzamento veloce è limitato a 8.
* Quando si utilizzano adattamenti di gioco trucco per fornire la modalità trucco, la traccia audio è disabilitata.
* In modalità di riproduzione a trucco, la commutazione di tracce audio e sottotitoli è disattivata.
* La riproduzione e la pausa sono abilitate.
* Al momento della ricerca, se la riproduzione è in modalità di riproduzione con trucco, la velocità di riproduzione è impostata su 1 e la riproduzione normale riprende.
* La logica del bit rate adattivo (ABR) è abilitata.

   Quando si utilizzano gli adattamenti normali, i profili sono limitati tra `ABRControlParameters.minBitRate` e `ABRControlParameters.maxBitRate`. Quando si utilizzano adattamenti per la riproduzione di trucco, i profili sono limitati tra `ABRControlParameters.minTrickPlayBitRate` e `ABRControlParameters.maxTrickPlayBitRate`.