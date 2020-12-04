---
description: Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
seo-description: Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.
seo-title: Implementazione rapida in avanti e indietro
title: Implementazione rapida in avanti e indietro
uuid: bd190534-c871-4673-b79d-1413277f480f
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---


# Implementazione rapida in avanti e riavvolgimento {#implement-fast-forward-and-rewind}

Quando gli utenti avanzano velocemente o riavvolgono rapidamente i supporti, si trovano in modalità di riproduzione trucco. Per passare alla modalità di riproduzione a trucco, è necessario impostare la velocità di riproduzione di MediaPlayer su un valore diverso da 1.

Per cambiare la velocità, è necessario impostare un valore.

1. Passa dalla modalità di riproduzione normale (1x) alla modalità di riproduzione ingannevole impostando la proprietà `rate` su un valore consentito.`MediaPlayer`

   * La classe `MediaPlayerItem` definisce le frequenze di riproduzione consentite.
   * TVSDK seleziona la tariffa più vicina consentita se la frequenza specificata non è consentita.

      Quando la frequenza di trickplay viene modificata da 0 (pausa) o 1 (riproduzione normale) a una velocità maggiore di 1 o inferiore a -1, tutti gli annunci sulla timeline vengono rimossi. L&#39;intera timeline dispone di un solo punto che semplifica un&#39;azione di trickplay per consentire al contenuto di essere inoltrato rapidamente e riavvolto senza fermarsi a nessuna posizione dell&#39;annuncio. Questa azione è abilitata da un&#39;azione di distacco della timeline su TVSDK per rimuovere tutti gli adBreaks risolti. Quando la riproduzione del trickplay riprende a 0 o 1, gli adBreaks vengono prima ripristinati dall’azione dell’allegato della timeline.

      Ricorda le seguenti informazioni:

   * Se l’azione di trickplay consiste nel riavvolgere il contenuto, la riproduzione riprende quando la frequenza viene modificata in 1.
   * Se l’azione di trickplay consente di avanzare rapidamente il contenuto, l’ultima azione adBreak saltata viene riprodotta nella posizione di ripresa.

   In questo esempio, la frequenza di riproduzione interna del lettore viene impostata sulla frequenza richiesta.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Facoltativamente, puoi ascoltare gli eventi relativi ai cambiamenti di tasso, che ti permettono di sapere quando hai richiesto un cambiamento di tasso e quando un cambiamento di tasso si verifica effettivamente.

   TVSDK invia gli eventi seguenti relativi al trucco:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` quando il  `rate` valore cambia in un altro valore.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` quando la riproduzione riprende alla frequenza selezionata.

   TVSDK invia entrambi questi eventi quando il lettore ritorna dalla modalità di riproduzione a quella normale.

## Elementi API Rate Change {#rate-change-api}

TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.

Utilizzate i seguenti elementi API per modificare le percentuali di riproduzione:

* `MediaPlayer.rate` con funzioni setter e getter
* `MediaPlayer.localTime property` con funzione getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` proprietà con funzione getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` con funzione getter - specifica le frequenze valide.

| Valore rate | Effetto sulla riproduzione |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più veloce del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2,0, -4,0, -8,0, -16,0, -32,0, -64,0, -128,0 | Passa alla modalità di riavvolgimento rapido |
| 1,0 | Passa alla modalità di riproduzione normale (la chiamata di `play` equivale a impostare la proprietà rate su 1.0) |
| 0,0 | Pauses (la chiamata di `pause` equivale all&#39;impostazione della proprietà rate su 0.0) |

## Limitazioni e comportamento per il gioco trucco {#limitations-behavior-trick-play}

Di seguito sono riportati i limiti per la modalità di riproduzione trucco:

* La playlist principale deve contenere segmenti di solo I-frame. Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia I-frame.
* La traccia audio e i sottotitoli codificati sono disattivati.
* La logica ABR (Adaptive Bit Rate) è disabilitata. TVSDK seleziona un bitrate compreso tra il valore più basso tra il valore di bitrate fornito e 800 kbps e lo utilizza per l’intera sessione di trucco.
* Riproduci e Pausa sono abilitati.
* La ricerca è proibita. Per effettuare una ricerca, chiamare `pause` per uscire dalla modalità di riproduzione trucco e chiamare `seek`.

* È possibile uscire dalla modalità &quot;trucco-play&quot; a qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile eseguire il trucco solo durante la riproduzione del contenuto principale. Viene inviato un errore se si tenta di passare alla riproduzione ingannevole durante un&#39;interruzione di annuncio.
   * Dopo l’inizio della modalità di riproduzione trucco, le interruzioni di annunci vengono ignorate e non vengono attivati eventi di annunci.
   * La timeline esposta da TVSDK all’applicazione del lettore non viene modificata anche se vengono ignorate le interruzioni pubblicitarie.
   * La proprietà `MediaPlayer.currentTime` passa in avanti (in avanti veloce) o indietro (in seguito a riavvolgimento rapido) con la durata dell&#39;interruzione annuncio saltata. Questo comportamento di salto per il tempo corrente consente di mantenere invariata la durata del flusso durante la riproduzione del trucco. L&#39;applicazione del lettore può utilizzare la proprietà `localTime` per tenere traccia dell&#39;ora relativa solo al contenuto principale. Non viene eseguito alcun salto di ora sui valori restituiti per l&#39;ora locale quando si salta un annuncio.

   * L&#39;evento `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un&#39;interruzione pubblicitaria stia per essere ignorata. Il lettore può utilizzare questo evento per implementare la logica personalizzata relativa alle interruzioni pubblicitarie saltate.
   * L’uscita dalla riproduzione trucco richiama lo stesso criterio di riproduzione degli annunci applicato all’uscita dalla ricerca.

      Pertanto, come nella ricerca, il comportamento dipende dal fatto che il criterio di riproduzione dell&#39;applicazione sia diverso da quello predefinito. L&#39;impostazione predefinita prevede che l&#39;ultima interruzione annuncio saltata venga riprodotta nel punto in cui si esce dal gioco di trucco.