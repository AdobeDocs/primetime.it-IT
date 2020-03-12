---
description: Ci sono alcuni limiti e alcuni problemi nel modo in cui la modalità di gioco trucco si comporta.
seo-description: Ci sono alcuni limiti e alcuni problemi nel modo in cui la modalità di gioco trucco si comporta.
seo-title: Limitazioni e comportamento per il gioco di trucchi
title: Limitazioni e comportamento per il gioco di trucchi
uuid: 0e84c9ef-fc18-4667-ad17-7f4777b552ba
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Limitazioni e comportamento per il gioco di trucchi{#limitations-and-behavior-for-trick-play}

Ci sono alcuni limiti e alcuni problemi nel modo in cui la modalità di gioco trucco si comporta.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Di seguito sono riportati i limiti per la modalità di riproduzione trucco:

* La playlist principale deve contenere segmenti di solo I-frame. Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia I-frame.
* La traccia audio e i sottotitoli codificati sono disattivati.
* La logica ABR (Adaptive Bit Rate) è disabilitata. TVSDK seleziona un bitrate compreso tra il valore più basso tra il valore di bitrate fornito e 800 kbps e lo utilizza per l’intera sessione di trucco.
* Riproduci e Pausa sono abilitati.
* La ricerca è proibita. Per cercare, chiamare `pause` per uscire dalla modalità di gioco trucco e chiamare `seek`.

* È possibile passare dalla modalità di riproduzione a qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile eseguire il trucco solo durante la riproduzione del contenuto principale. Viene inviato un errore se si tenta di passare alla riproduzione ingannevole durante un&#39;interruzione di annuncio.
   * Dopo l’inizio della modalità di riproduzione trucco, le interruzioni di annunci vengono ignorate e non vengono attivati eventi di annunci.
   * La timeline esposta da TVSDK all’applicazione del lettore non viene modificata anche se vengono ignorate le interruzioni pubblicitarie.
   * Il valore temporale corrente passa in avanti (in avanti veloce) o indietro (in riavvolgimento rapido) con la durata dell’interruzione annuncio saltata. Questo comportamento di salto per il tempo corrente consente di mantenere invariata la durata del flusso durante la riproduzione del trucco. L’applicazione di riproduzione può ottenere il valore dell’ora locale per tenere traccia dell’ora solo rispetto al contenuto principale. Non viene eseguito alcun salto di ora sui valori restituiti per l&#39;ora locale quando si salta un annuncio.
   * L&#39; `MediaPlayerEvent.AD_BREAK_SKIPPED` evento viene inviato immediatamente prima che un&#39;interruzione pubblicitaria stia per essere saltata. Il lettore può utilizzare questo evento per implementare la logica personalizzata relativa alle interruzioni pubblicitarie saltate.
   * L’uscita dalla riproduzione trucco richiama lo stesso criterio di riproduzione degli annunci applicato all’uscita dalla ricerca.

      Pertanto, come nella ricerca, il comportamento dipende dal fatto che il criterio di riproduzione dell&#39;applicazione sia diverso da quello predefinito. L&#39;impostazione predefinita prevede che l&#39;ultima interruzione annuncio saltata venga riprodotta nel punto in cui si esce dalla modalità di gioco trucco.

