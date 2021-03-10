---
title: Limitazioni e comportamento per il gioco a tre
description: Limitazioni e comportamento per il gioco a tre
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Limitazioni e comportamento per il gioco a tre {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitazioni per la modalità di gioco trucco:

* La playlist principale deve contenere segmenti solo Iframe.

   Sullo schermo vengono visualizzati solo i fotogrammi chiave della traccia Iframe.
* La traccia audio e i sottotitoli sono disattivati.
* La riproduzione e la pausa sono abilitate.
* È possibile uscire dalla modalità di riproduzione a tre tasti in qualsiasi velocità di riproduzione consentita (riproduzione o pausa).
* Quando gli annunci sono incorporati nel flusso:

   * È possibile andare a giocare a trucco solo durante la riproduzione del contenuto principale. Viene inviato un errore se si tenta di passare alla riproduzione di un trucco durante una pausa pubblicitaria.
   * Dopo aver avviato la modalità di riproduzione a trucco, le interruzioni di annunci vengono ignorate e non vengono attivati eventi di annunci.
   * La timeline esposta da TVSDK al lettore non viene modificata anche se vengono saltate le interruzioni pubblicitarie.
   * Il valore del tempo corrente salta in avanti (in avanti veloce) o indietro (in riavvolgimento rapido) con la durata dell&#39;annuncio saltato.

      Questo comportamento di salto per l&#39;ora corrente consente alla durata del flusso di rimanere inalterata durante il gioco di trucco. Il lettore può tenere traccia del tempo relativo solo al contenuto principale. Non vengono eseguiti salti di tempo sui valori restituiti per l’ora locale quando si salta un annuncio.
   * L’evento `MediaPlayerEvent.AD_BREAK_SKIPPED` viene inviato immediatamente prima che un’interruzione pubblicitaria venga ignorata.

      Il lettore può utilizzare questo evento per implementare una logica personalizzata relativa alle interruzioni pubblicitarie saltate.

   * L&#39;uscita dalla riproduzione di un trucco richiama lo stesso criterio di riproduzione dell&#39;annuncio utilizzato per uscire dalla ricerca.

      Come per la ricerca, il comportamento dipende dal fatto che i criteri di riproduzione dell’applicazione siano diversi da quelli predefiniti. Il valore predefinito è che l&#39;ultima interruzione pubblicitaria saltata viene giocata nel punto in cui si esce fuori gioco di trucco.

