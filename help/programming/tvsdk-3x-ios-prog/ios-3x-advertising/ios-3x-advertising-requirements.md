---
description: Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l'interfaccia  Adobe Primetime e decisionali.
seo-description: Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l'interfaccia  Adobe Primetime e decisionali.
seo-title: Requisiti di pubblicità
title: Requisiti di pubblicità
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Requisiti di pubblicità {#advertising-requirements}

Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l&#39;interfaccia  Adobe Primetime e decisionali.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime ad Decioning funziona con TVSDK per identificare opportunità di annunci, risolvere annunci e inserire annunci risolti nei flussi video.

Per includere annunci nel contenuto video, accertatevi che la pubblicità e il contenuto video principale soddisfino i seguenti requisiti:

* La versione HLS del contenuto pubblicitario non può essere superiore alla versione HLS del contenuto principale.
* Gli annunci devono essere multiplexati e contenere una rappresentazione solo audio, indipendentemente dal fatto che il contenuto principale sia multiplexato.
* Le playlist degli annunci devono avere le stesse rappresentazioni con bitrate delle rappresentazioni nella playlist del contenuto principale.
* La durata di destinazione e la durata del singolo frammento di un annuncio non possono superare la durata di destinazione del contenuto principale.
* Se il contenuto principale contiene un flusso solo audio, il contenuto pubblicitario deve contenere anche un flusso solo audio.
* Se il contenuto principale contiene flussi di sottotitoli, il contenuto pubblicitario deve essere non crittografato.
* Se il contenuto principale è un bit rate multiplo (MBR), anche il contenuto pubblicitario deve essere MBR.
* Se il contenuto principale dispone di tracce audio alternative, ogni annuncio deve avere almeno un flusso solo audio.

Se l’annuncio non dispone di almeno un flusso solo audio, l’annuncio viene ignorato.