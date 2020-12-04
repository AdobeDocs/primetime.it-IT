---
description: 'null'
seo-description: 'null'
seo-title: Limitazioni e comportamento per il gioco di trucchi
title: Limitazioni e comportamento per il gioco di trucchi
uuid: c28cc8db-3f45-488e-ab72-b102b3a1fab2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Limitazioni e comportamento per il gioco trucco {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limiti per la modalità di gioco trucco:

* La playlist principale deve contenere segmenti solo Iframe.

   Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia Iframe.
* La traccia audio e i sottotitoli codificati sono disattivati.
* Riproduci e Pausa sono abilitati.
* È possibile uscire dalla modalità &quot;trucco-play&quot; a qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile eseguire il trucco solo durante la riproduzione del contenuto principale. Viene inviato un errore se si tenta di passare alla riproduzione ingannevole durante un&#39;interruzione di annuncio.
   * Dopo aver avviato la modalità di riproduzione trucco, le interruzioni di annunci vengono ignorate e non vengono attivati eventi di annunci.
   * La timeline esposta da TVSDK al lettore non viene modificata anche se vengono ignorate le interruzioni pubblicitarie.
   * Il valore temporale corrente passa in avanti (in avanti veloce) o indietro (in riavvolgimento rapido) con la durata dell’interruzione annuncio saltata.

      Questo comportamento di salto per il tempo corrente consente di mantenere invariata la durata del flusso durante la riproduzione del trucco. Il lettore può tenere traccia della durata solo rispetto al contenuto principale. Non viene eseguito alcun salto di ora sui valori restituiti per l&#39;ora locale quando si salta un annuncio.
   * L&#39;evento `MediaPlayerEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un&#39;interruzione pubblicitaria stia per essere ignorata.

      Il lettore può utilizzare questo evento per implementare la logica personalizzata relativa alle interruzioni pubblicitarie saltate.

   * L’uscita dalla riproduzione trucco richiama lo stesso criterio di riproduzione degli annunci applicato all’uscita dalla ricerca.

      Come per la ricerca, il comportamento dipende dal fatto che il criterio di riproduzione dell&#39;applicazione sia diverso da quello predefinito. L&#39;impostazione predefinita prevede che l&#39;ultima interruzione annuncio saltata venga riprodotta nel punto in cui si esce dal gioco di trucco.