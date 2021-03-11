---
title: Requisiti in materia di pubblicità
description: Requisiti in materia di pubblicità
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Requisiti per la pubblicità {#advertising-requirements}

Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l&#39;interfaccia Adobe Primetime ad Decioning.

Primetime ad decisioning funziona con TVSDK per identificare le opportunità degli annunci, risolvere gli annunci e inserire annunci risolti nei flussi video.

Per incorporare annunci nei contenuti video, accertati che il contenuto pubblicitario e video principale soddisfi i seguenti requisiti:

* La versione HLS del contenuto pubblicitario non può essere superiore alla versione HLS del contenuto principale.
* Gli annunci devono essere multiplex e devono contenere un rendering solo audio, indipendentemente dal fatto che il contenuto principale sia multiplexato.
* Le playlist degli annunci devono avere le stesse rappresentazioni a bit rate delle rappresentazioni nella playlist dei contenuti principali.
* La durata di destinazione e la durata del singolo frammento di un annuncio non possono superare la durata di destinazione del contenuto principale.
* Se il contenuto principale contiene un flusso solo audio, il contenuto pubblicitario deve contenere anche un flusso solo audio.
* Se il contenuto principale contiene flussi di sottotitoli, il contenuto pubblicitario deve essere non crittografato.
* Se il contenuto principale è a bit rate multiplo (MBR), anche il contenuto pubblicitario deve essere MBR.
* Se il contenuto principale dispone di tracce audio alternative, ogni annuncio deve avere almeno un flusso solo audio.

   Se l’annuncio non dispone di almeno un flusso solo audio, l’annuncio viene ignorato.