---
description: Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning.
title: Requisiti pubblicitari
exl-id: 164a5e79-1634-4853-a2b9-d4b5bdbbf190
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Requisiti pubblicitari {#advertising-requirements}

Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning.

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime ad decisioning funziona con TVSDK per identificare opportunità pubblicitarie, risolvere annunci e inserire annunci risolti nei flussi video.

Per incorporare gli annunci nel contenuto video, assicurati che il contenuto pubblicitario e il contenuto video principale soddisfino i seguenti requisiti:

* La versione HLS del contenuto pubblicitario non può essere superiore alla versione HLS del contenuto principale.
* Gli annunci devono essere multiplexati e devono contenere una rappresentazione solo audio, indipendentemente dal fatto che il contenuto principale sia multiplexato.
* Le playlist degli annunci devono avere le stesse rappresentazioni a bit-rate delle rappresentazioni nella playlist del contenuto principale.
* La durata di destinazione e la durata di un singolo frammento di un annuncio non possono superare la durata di destinazione del contenuto principale.
* Se il contenuto principale contiene uno streaming solo audio, anche il contenuto pubblicitario deve contenere uno streaming solo audio.
* Se il contenuto principale contiene flussi di sottotitoli, il contenuto pubblicitario deve essere non crittografato.
* Se il contenuto principale è il bitrate multiplo (MBR), anche il contenuto pubblicitario deve essere MBR.
* Se il contenuto principale ha tracce audio alternative, ogni annuncio deve avere almeno un flusso solo audio, altrimenti gli annunci devono essere demussi. Se l’annuncio non dispone di almeno un flusso di sola audio né è demussato, l’annuncio viene saltato.
