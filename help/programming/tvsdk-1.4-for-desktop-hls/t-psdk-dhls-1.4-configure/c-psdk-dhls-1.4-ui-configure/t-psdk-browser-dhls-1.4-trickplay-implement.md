---
description: Quando l'utente avanza o riavvolge rapidamente il supporto, si trova nella modalità di riproduzione con trucco. Per accedere alla modalità di riproduzione con trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
title: Implementazione di avanzamento rapido e riavvolgimento
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Implementazione di avanzamento rapido e riavvolgimento {#implement-fast-forward-and-rewind}

Quando l&#39;utente avanza o riavvolge rapidamente il supporto, si trova nella modalità di riproduzione con trucco. Per accedere alla modalità di riproduzione con trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

Per cambiare la velocità, è necessario impostare un valore.

1. Passare dalla modalità di riproduzione normale (1x) alla modalità di riproduzione con trazione impostando `rate` proprietà sul `MediaPlayer` a un valore consentito.

   * Il `MediaPlayerItem` classe definisce le velocità di riproduzione consentite.
   * Se la tariffa specificata non è consentita, TVSDK seleziona la tariffa consentita più vicina.

      Quando la frequenza di trickplay viene cambiata da 0 (pausa) o 1 (riproduzione normale) a una frequenza maggiore di 1 o minore di -1, tutti gli annunci sulla timeline vengono rimossi. È disponibile un solo punto sull’intera timeline che facilita un’azione di trickplay per consentire di inoltrare e riavvolgere rapidamente il contenuto senza fermarsi in nessuna posizione dell’annuncio. Questa azione è abilitata da un’azione di distacco della timeline su TVSDK per rimuovere tutti gli adBreak risolti. Quando la riproduzione trickplay riprende a 0 o 1, gli adBreaks vengono ripristinati per la prima volta dall’azione di allegato della timeline.

      Tenere presenti le seguenti informazioni:

   * Se l’azione di trickplay consiste nel riavvolgere il contenuto, la riproduzione riprende quando la frequenza viene modificata in 1.
   * Se l’azione di trickplay consiste nell’avanzare rapidamente il contenuto, l’ultimo adBreak saltato viene riprodotto nella posizione di ripresa.

   Questo esempio imposta la velocità di riproduzione interna del lettore sulla velocità richiesta.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Facoltativamente, è possibile ascoltare gli eventi di variazione di tasso, che consentono di sapere quando è stata richiesta una modifica di tasso e quando si verifica effettivamente una modifica di tasso.

   TVSDK invia i seguenti eventi relativi alla riproduzione con trucco:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` quando `rate` il valore viene modificato in un valore diverso.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` quando la riproduzione riprende alla velocità selezionata.

   TVSDK invia entrambi questi eventi quando il lettore ritorna dalla modalità di riproduzione con trucco alla modalità di riproduzione normale.

## Elementi API per la modifica della velocità {#rate-change-api}

TVSDK include metodi, proprietà ed eventi per determinare i tassi validi, i tassi correnti, se è supportata la riproduzione con trucco e altre funzionalità correlate all&#39;avanzamento e al riavvolgimento rapido.

Utilizza i seguenti elementi API per modificare le percentuali di riproduzione:

* `MediaPlayer.rate` proprietà con funzioni di impostazione e getter
* `MediaPlayer.localTime property` con funzione getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` proprietà con funzione getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` proprietà con funzione getter - specifica tassi validi.

| Valore tariffa | Effetto sulla riproduzione |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più rapidamente del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | Passa alla modalità di riavvolgimento rapido |
| 1.0 | Passa alla modalità di riproduzione normale (chiamata `play` equivale a impostare la proprietà rate su 1,0) |
| 0.0 | Pause (chiamata `pause` equivale a impostare la proprietà rate su 0,0) |

## Limitazioni e comportamento per la riproduzione con trucco {#limitations-behavior-trick-play}

Di seguito sono riportate le limitazioni relative alla modalità di riproduzione con trucco:

* La playlist master deve contenere segmenti di solo I-frame. Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia I-frame.
* La traccia audio e i sottotitoli sono disattivati.
* La logica ABR (Adaptive Bit Rate) è disabilitata. TVSDK seleziona una velocità in bit tra la velocità più bassa fornita e 800 kbps e utilizza tale velocità durante l’intera sessione di trick-play.
* Riproduci e pausa sono attivati.
* Ricerca non consentita. Per cercare, chiama `pause` per uscire dalla modalità di riproduzione con trucco e chiamare `seek`.

* È possibile uscire dalla modalità di riproduzione con trick-play in qualsiasi frequenza di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile eseguire il trucco solo durante la riproduzione del contenuto principale. Se tenti di passare alla riproduzione con trucco durante un’interruzione pubblicitaria, viene inviato un errore.
   * Dopo aver avviato la modalità di riproduzione con trucco, le interruzioni pubblicitarie vengono ignorate e non vengono generati eventi pubblicitari.
   * La timeline esposta da TVSDK all’applicazione del lettore non viene modificata anche se vengono saltate le interruzioni pubblicitarie.
   * Il `MediaPlayer.currentTime` La proprietà si sposta in avanti (su avanzamento rapido) o all’indietro (su riavvolgimento rapido) con la durata dell’interruzione pubblicitaria saltata. Questo comportamento di salto per l&#39;ora corrente consente alla durata del flusso di rimanere invariata durante la riproduzione con il trucco. L&#39;applicazione del lettore può utilizzare `localTime` per tenere traccia del tempo relativo solo al contenuto principale. Non vengono eseguiti salti di ora sui valori restituiti per l’ora locale quando si salta un annuncio.

   * Il `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un’interruzione pubblicitaria stia per essere ignorata. Il lettore può utilizzare questo evento per implementare una logica personalizzata relativa alle interruzioni pubblicitarie saltate.
   * L’uscita dalla modalità di riproduzione con trucco richiama lo stesso criterio di riproduzione degli annunci utilizzato all’uscita dalla ricerca.

      Pertanto, come nella ricerca, il comportamento dipende dal fatto che i criteri di riproduzione dell’applicazione siano diversi da quelli predefiniti. L’impostazione predefinita prevede che l’ultima interruzione pubblicitaria saltata venga riprodotta nel punto in cui si esce dalla riproduzione con i trucchi.
