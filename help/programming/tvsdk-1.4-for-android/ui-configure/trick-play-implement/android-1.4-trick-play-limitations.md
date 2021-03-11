---
description: Ci sono alcune limitazioni e alcuni problemi nel modo in cui si comporta la modalità di gioco trucco.
title: Limitazioni e comportamento per il gioco a tre
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Limitazioni e comportamento per i giochi con trucchi{#limitations-and-behavior-for-trick-play}

Ci sono alcune limitazioni e alcuni problemi nel modo in cui si comporta la modalità di gioco trucco.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Di seguito sono riportati i limiti per la modalità di gioco trucco:

* La playlist principale deve contenere segmenti solo i-frame. Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia I-frame.
* La traccia audio e i sottotitoli sono disattivati.
* La logica del bit rate adattivo (ABR) è disabilitata. TVSDK seleziona un bit rate tra il più basso tasso fornito e 800 kbps e lo utilizza durante l&#39;intera sessione di trucco-play.
* La riproduzione e la pausa sono abilitate.
* Cercare è inammissibile. Per cercare, chiama `pause` per uscire dalla modalità di riproduzione dei trucchi e poi chiama `seek`.

* È possibile passare dalla modalità di riproduzione con trucco a qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile andare a giocare a trucco solo durante la riproduzione del contenuto principale. Viene inviato un errore se si tenta di passare alla riproduzione di un trucco durante una pausa pubblicitaria.
   * Dopo aver iniziato la modalità di riproduzione a trucco, le interruzioni di annunci vengono ignorate e non vengono attivati eventi di annunci.
   * La timeline esposta da TVSDK all’applicazione del lettore non viene modificata anche se vengono saltate le interruzioni pubblicitarie.
   * Il valore del tempo corrente salta in avanti (in avanti veloce) o indietro (in riavvolgimento rapido) con la durata dell&#39;annuncio saltato. Questo comportamento di salto per l&#39;ora corrente consente alla durata del flusso di rimanere inalterata durante il gioco di trucco. L’applicazione di riproduzione può ottenere il valore dell’ora locale per tenere traccia dell’ora relativa solo al contenuto principale. Non vengono eseguiti salti di tempo sui valori restituiti per l’ora locale quando si salta un annuncio.
   * L’evento `MediaPlayerEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un’interruzione pubblicitaria venga ignorata. Il lettore può utilizzare questo evento per implementare una logica personalizzata relativa alle interruzioni pubblicitarie saltate.
   * L&#39;uscita dalla riproduzione di un trucco richiama lo stesso criterio di riproduzione dell&#39;annuncio utilizzato per uscire dalla ricerca.

      Pertanto, come nella ricerca, il comportamento dipende dal fatto che i criteri di riproduzione dell’applicazione siano diversi da quelli predefiniti. L&#39;impostazione predefinita prevede che l&#39;ultima interruzione pubblicitaria saltata venga riprodotta nel punto in cui si esce dalla modalità di gioco trabocchetto.

