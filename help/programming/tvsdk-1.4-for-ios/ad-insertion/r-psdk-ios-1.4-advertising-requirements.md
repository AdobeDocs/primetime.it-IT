---
title: Requisiti pubblicitari
description: Requisiti pubblicitari
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Requisiti pubblicitari {#advertising-requirements}

Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning.

Primetime ad decisioning funziona con TVSDK per identificare opportunità pubblicitarie, risolvere annunci e inserire annunci risolti nei flussi video.

Per incorporare gli annunci nel contenuto video, assicurati che il contenuto pubblicitario e il contenuto video principale soddisfino i seguenti requisiti:

* La versione HLS del contenuto pubblicitario non può essere superiore alla versione HLS del contenuto principale.
* Gli annunci devono essere multiplexati e devono contenere una rappresentazione solo audio, indipendentemente dal fatto che il contenuto principale sia multiplexato.
* Le playlist degli annunci devono avere le stesse rappresentazioni a bit-rate delle rappresentazioni nella playlist del contenuto principale.
* La durata di destinazione e la durata di un singolo frammento di un annuncio non possono superare la durata di destinazione del contenuto principale.
* Se il contenuto principale contiene uno streaming solo audio, anche il contenuto pubblicitario deve contenere uno streaming solo audio.
* Se il contenuto principale contiene flussi di sottotitoli, il contenuto pubblicitario deve essere non crittografato.
* Se il contenuto principale è il bitrate multiplo (MBR), anche il contenuto pubblicitario deve essere MBR.
* Se il contenuto principale ha tracce audio alternative, ogni annuncio deve avere almeno un flusso solo audio.

  Se l’annuncio non dispone di almeno un flusso solo audio, l’annuncio viene saltato.
