---
title: Usare  Ad Insertion nel flusso Live/Linear
description: Utilizzo  Ad Insertion nel flusso Live/Linear
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Utilizzare  Ad Insertion nel flusso Live/Linear {#ad-insertion-live-linear-stream}

Primetime  Ad Insertion offre agli editori la possibilità di gestire situazioni di inserimento di annunci standard e complessi che si verificano durante i flussi live/lineari.

## Formati Cue supportati {#cue-formats-supported}

Primetime  Ad Insertion supporta un&#39;ampia gamma di formati cue standard e non standard, tra cui:

* DPI SCTE-35 (indicatori di annunci avanzati SCTE-35)

* [ Adobe Digital Program Insertion Signaling Specification](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* Binario SCTE-35 (sia HLS che DASH)

* SCTE-35 testuale (sia HLS che DASH)

Per ulteriori informazioni o per altri formati di cue point supportati, contattate il vostro rappresentante di supporto Primetime.

## Supporto per interruzioni pubblicitarie parziali {#partial-ad-break-support}

Le interruzioni pubblicitarie parziali possono essere utilizzate nelle situazioni in cui un visualizzatore immette un flusso live/lineare dopo l&#39;inizio di un&#39;interruzione di annuncio.  Ad esempio, se un visualizzatore immette un&#39;interruzione pubblicitaria lunga 2:00 al punto 1:00, l&#39;inserimento parziale dell&#39;annuncio assicurerà che gli annunci vengano serviti nel tempo rimanente. Senza l&#39;inserimento parziale di un&#39;interruzione pubblicitaria, durante l&#39;interruzione il visualizzatore non riceve alcun annuncio. Primetime  Ad Insertion abilita l&#39;inserimento parziale di un&#39;interruzione pubblicitaria per impostazione predefinita se i tag appropriati sono presenti nei flussi multimediali.

## Ritorno anticipato (uscita annuncio anticipato) {#early-return-early-ad-exit}

In alcuni casi potrebbe essere necessario tornare presto da un&#39;interruzione pubblicitaria in un flusso live/lineare, ad esempio quando un evento sportivo improvvisamente ritorna all&#39;azione. Ogni formato di decisione degli annunci contiene un tag per &quot;cue-out&quot; (annunci) o &quot;cue-in&quot; (contenuto).  Se prima della fine di un&#39;interruzione dell&#39;annuncio viene rilevato un tag &quot;cue-in&quot;,  Adobe Primetime  Ad Insertion onorerà il cue-in.  Contattate il Content Packager per abilitare la restituzione anticipata.
