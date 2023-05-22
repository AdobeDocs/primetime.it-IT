---
title: Limitazioni e comportamento per la riproduzione con trucco
description: Limitazioni e comportamento per la riproduzione con trucco
copied-description: true
exl-id: 5d9cae7b-d850-4ebc-8780-5abec847bb82
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Limitazioni e comportamento per la riproduzione con trucco {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limiti per la modalità di riproduzione con trucco:

* La playlist master deve contenere segmenti solo Iframe.

   Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia Iframe.
* La traccia audio e i sottotitoli sono disattivati.
* Riproduci e pausa sono attivati.
* È possibile uscire dalla modalità di riproduzione con trick-play in qualsiasi frequenza di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile eseguire il trucco solo durante la riproduzione del contenuto principale. Se tenti di passare alla riproduzione con trucco durante un’interruzione pubblicitaria, viene inviato un errore.
   * Dopo aver avviato la modalità di riproduzione con trucco, le interruzioni pubblicitarie vengono ignorate e non vengono generati eventi pubblicitari.
   * La timeline esposta da TVSDK al lettore non viene modificata anche se vengono saltate le interruzioni pubblicitarie.
   * Il valore di tempo corrente passa in avanti (su avanzamento rapido) o indietro (su riavvolgimento rapido) con la durata dell’interruzione pubblicitaria saltata.

      Questo comportamento di salto per l&#39;ora corrente consente alla durata del flusso di rimanere invariata durante la riproduzione con il trucco. Il lettore può tracciare il tempo relativo solo al contenuto principale. Non vengono eseguiti salti di ora sui valori restituiti per l’ora locale quando si salta un annuncio.
   * Il `MediaPlayerEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un’interruzione pubblicitaria stia per essere ignorata.

      Il lettore può utilizzare questo evento per implementare una logica personalizzata relativa alle interruzioni pubblicitarie saltate.

   * L’uscita dalla modalità di riproduzione con trucco richiama lo stesso criterio di riproduzione degli annunci utilizzato all’uscita dalla ricerca.

      Come per la ricerca, il comportamento dipende dalla differenza tra i criteri di riproduzione dell’applicazione e quelli predefiniti. L’impostazione predefinita prevede che l’ultima interruzione pubblicitaria saltata venga riprodotta nel punto in cui si esce dalla riproduzione con i trucchi.
