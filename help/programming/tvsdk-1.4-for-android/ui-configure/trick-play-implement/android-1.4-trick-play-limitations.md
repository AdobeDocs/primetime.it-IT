---
description: Ci sono alcune limitazioni e alcuni problemi nel modo in cui la modalità di riproduzione con trucco si comporta.
title: Limitazioni e comportamento per la riproduzione con trucco
exl-id: 98558970-9e5e-4dc1-a327-63d9db1d4fed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Limitazioni e comportamento per la riproduzione con trucco{#limitations-and-behavior-for-trick-play}

Ci sono alcune limitazioni e alcuni problemi nel modo in cui la modalità di riproduzione con trucco si comporta.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Di seguito sono riportate le limitazioni della modalità di riproduzione con trucco:

* La playlist master deve contenere segmenti di solo I-frame. Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia I-frame.
* La traccia audio e i sottotitoli sono disattivati.
* La logica ABR (Adaptive Bit Rate) è disabilitata. TVSDK seleziona una velocità in bit tra la velocità più bassa fornita e 800 kbps e utilizza tale velocità durante l’intera sessione di trick-play.
* Riproduci e pausa sono attivati.
* Ricerca non consentita. Per cercare, chiama `pause` per uscire dalla modalità di riproduzione con trucco e chiamare `seek`.

* È possibile passare dalla modalità di riproduzione con trucco a qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile eseguire il trucco solo durante la riproduzione del contenuto principale. Se tenti di passare alla riproduzione con trucco durante un’interruzione pubblicitaria, viene inviato un errore.
   * Dopo aver avviato la modalità di riproduzione con trucco, le interruzioni pubblicitarie vengono ignorate e non vengono generati eventi pubblicitari.
   * La timeline esposta da TVSDK all’applicazione del lettore non viene modificata anche se vengono saltate le interruzioni pubblicitarie.
   * Il valore di tempo corrente passa in avanti (su avanzamento rapido) o indietro (su riavvolgimento rapido) con la durata dell’interruzione pubblicitaria saltata. Questo comportamento di salto per l&#39;ora corrente consente alla durata del flusso di rimanere invariata durante la riproduzione con il trucco. L’applicazione lettore può ottenere il valore dell’ora locale per tracciare l’ora relativa solo al contenuto principale. Non vengono eseguiti salti di ora sui valori restituiti per l’ora locale quando si salta un annuncio.
   * Il `MediaPlayerEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un’interruzione pubblicitaria stia per essere ignorata. Il lettore può utilizzare questo evento per implementare una logica personalizzata relativa alle interruzioni pubblicitarie saltate.
   * L’uscita dalla modalità di riproduzione con trucco richiama lo stesso criterio di riproduzione degli annunci utilizzato all’uscita dalla ricerca.

      Pertanto, come nella ricerca, il comportamento dipende dal fatto che i criteri di riproduzione dell’applicazione siano diversi da quelli predefiniti. L’impostazione predefinita prevede che l’ultima interruzione pubblicitaria saltata venga riprodotta nel punto in cui si esce dalla modalità di riproduzione con trucco.
