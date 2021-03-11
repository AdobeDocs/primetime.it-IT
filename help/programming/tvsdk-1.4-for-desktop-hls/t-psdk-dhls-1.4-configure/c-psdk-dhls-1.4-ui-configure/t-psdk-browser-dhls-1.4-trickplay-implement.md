---
description: Quando gli utenti avanzano velocemente o riavvolgono velocemente i contenuti multimediali, si trovano in modalità di riproduzione a trucco. Per accedere alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
title: Implementazione rapida in avanti e in riavvolgimento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# Implementa avanzamento rapido e riavvolgimento {#implement-fast-forward-and-rewind}

Quando gli utenti avanzano velocemente o riavvolgono velocemente i contenuti multimediali, si trovano in modalità di riproduzione a trucco. Per accedere alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

Per cambiare la velocità, è necessario impostare un valore.

1. Passa dalla modalità di riproduzione normale (1x) alla modalità di riproduzione con trucco impostando la proprietà `rate` su un valore consentito.`MediaPlayer`

   * La classe `MediaPlayerItem` definisce le velocità di riproduzione consentite.
   * TVSDK seleziona la velocità consentita più vicina se la velocità specificata non è consentita.

      Quando la frequenza di riproduzione viene modificata da 0 (pausa) o 1 (riproduzione normale) a una velocità maggiore di 1 o inferiore a -1, tutti gli annunci sulla timeline vengono rimossi. C&#39;è un solo periodo sull&#39;intera timeline che facilita un&#39;azione trickplay per consentire al contenuto di essere inoltrato rapidamente e riavvolto senza interruzioni in alcuna posizione pubblicitaria. Questa azione è abilitata da un’azione di distacco della timeline su TVSDK per rimuovere tutti gli adBreaks risolti. Quando il trickplay riprende a 0 o 1, gli adBreaks vengono prima ripristinati dall&#39;azione di attacco della timeline.

      Ricorda le seguenti informazioni:

   * Se l&#39;azione trickplay è quella di riavvolgere il contenuto, la riproduzione riprende quando la velocità viene modificata a 1.
   * Se l’azione trickplay è quella di inoltrare rapidamente il contenuto, l’ultima azione adBreak saltata viene riprodotta nella posizione di ripresa.

   In questo esempio la velocità di riproduzione interna del lettore viene impostata sulla velocità richiesta.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Facoltativamente, puoi ascoltare gli eventi di cambio di tasso, che ti permettono di sapere quando hai richiesto un cambiamento di tasso e quando un cambiamento di tasso si verifica effettivamente.

   TVSDK invia i seguenti eventi relativi al trucco:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` quando il  `rate` valore cambia in un valore diverso.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` quando la riproduzione riprende alla velocità selezionata.

   TVSDK invia entrambi questi eventi quando il lettore ritorna dalla modalità di gioco-trucco alla modalità di riproduzione normale.

## Elementi API di modifica della velocità {#rate-change-api}

TVSDK include metodi, proprietà ed eventi per determinare le percentuali valide, le percentuali correnti, se è supportata la riproduzione per trucco e altre funzionalità relative alla riavvolgimento e avanzamento rapido.

Utilizza i seguenti elementi API per modificare le percentuali di riproduzione:

* `MediaPlayer.rate` proprietà con funzioni setter e getter
* `MediaPlayer.localTime property` con funzione getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` proprietà con funzione getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` proprietà con funzione getter - specifica le percentuali valide.

| Valore rate | Effetto sulla riproduzione |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 , 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più rapidamente del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Passa alla modalità di riavvolgimento rapido |
| 1,0 | Passa alla modalità di riproduzione normale (chiamare `play` equivale a impostare la proprietà rate su 1.0) |
| 0,0 | Sospensioni (la chiamata di `pause` equivale all&#39;impostazione della proprietà rate su 0.0) |

## Limitazioni e comportamento per il gioco a tre {#limitations-behavior-trick-play}

Di seguito sono riportati i limiti per la modalità di gioco trucco:

* La playlist principale deve contenere segmenti solo i-frame. Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia I-frame.
* La traccia audio e i sottotitoli sono disattivati.
* La logica del bit rate adattivo (ABR) è disabilitata. TVSDK seleziona un bit rate tra il più basso tasso fornito e 800 kbps e lo utilizza durante l&#39;intera sessione di trucco-play.
* La riproduzione e la pausa sono abilitate.
* Cercare è inammissibile. Per cercare, chiama `pause` per uscire dalla modalità di riproduzione dei trucchi e poi chiama `seek`.

* È possibile uscire dalla modalità di riproduzione a tre tasti in qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile andare a giocare a trucco solo durante la riproduzione del contenuto principale. Viene inviato un errore se si tenta di passare alla riproduzione di un trucco durante una pausa pubblicitaria.
   * Dopo aver iniziato la modalità di riproduzione a trucco, le interruzioni di annunci vengono ignorate e non vengono attivati eventi di annunci.
   * La timeline esposta da TVSDK all’applicazione del lettore non viene modificata anche se vengono saltate le interruzioni pubblicitarie.
   * La proprietà `MediaPlayer.currentTime` salta in avanti (in avanti veloce) o indietro (in seguito a riavvolgimento rapido) con la durata dell&#39;interruzione pubblicitaria saltata. Questo comportamento di salto per l&#39;ora corrente consente alla durata del flusso di rimanere inalterata durante il gioco di trucco. L&#39;applicazione player può utilizzare la proprietà `localTime` per tenere traccia dell&#39;ora relativa solo al contenuto principale. Non vengono eseguiti salti di tempo sui valori restituiti per l’ora locale quando si salta un annuncio.

   * L’evento `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un’interruzione pubblicitaria venga ignorata. Il lettore può utilizzare questo evento per implementare una logica personalizzata relativa alle interruzioni pubblicitarie saltate.
   * L&#39;uscita dalla riproduzione di un trucco richiama lo stesso criterio di riproduzione dell&#39;annuncio utilizzato per uscire dalla ricerca.

      Pertanto, come nella ricerca, il comportamento dipende dal fatto che i criteri di riproduzione dell’applicazione siano diversi da quelli predefiniti. Il valore predefinito è che l&#39;ultima interruzione pubblicitaria saltata viene giocata nel punto in cui si esce fuori gioco di trucco.