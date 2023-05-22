---
title: Usa Ad Insertion in streaming live/lineare
description: Utilizzo dell’Ad Insertion in streaming live/lineare
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Usa Ad Insertion in streaming live/lineare {#ad-insertion-live-linear-stream}

Primetime Ad Insertion consente agli editori di gestire situazioni di inserimento di annunci standard e complessi che si verificano durante flussi live/lineari.

## Formati di cue supportati {#cue-formats-supported}

Primetime Ad Insertion supporta un’ampia gamma di formati cue standard e non standard, tra cui:

* DPI SCTE-35 (marcatori annuncio avanzati SCTE-35)

* [Adobe Digital Program Insertion Segnalazione Specifica](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* Binario SCTE-35 (sia HLS che DASH)

* Scte-35 testuale (sia HLS che DASH)

Contatta il rappresentante dell’assistenza Primetime per ulteriori dettagli o altri formati di cue supportati.

## Supporto parziale di Ad Break {#partial-ad-break-support}

Le interruzioni pubblicitarie parziali possono essere utilizzate in situazioni in cui lo spettatore entra in un flusso live/lineare dopo l’inizio di un’interruzione pubblicitaria.  Ad esempio, se un visualizzatore immette un’interruzione pubblicitaria lunga 2:00 al minuto 1:00, l’inserimento parziale dell’interruzione pubblicitaria assicura che gli annunci vengano trasmessi nel tempo rimanente. Senza l’inserimento parziale dell’interruzione pubblicitaria, questo visualizzatore non riceverebbe alcun annuncio durante l’interruzione. Primetime Ad Insertion abilita l’inserimento parziale dell’interruzione pubblicitaria per impostazione predefinita se i tag appropriati sono presenti nei flussi multimediali.

## Ritorno Anticipato (Uscita Anticipata Dall’Annuncio) {#early-return-early-ad-exit}

In alcuni casi può essere necessario tornare presto da un’interruzione pubblicitaria in un flusso live/lineare, ad esempio quando un evento sportivo ritorna improvvisamente in azione. Ogni formato di ad decisioning contiene un tag &quot;cue-out&quot; (annunci) o &quot;cue-in&quot; (contenuto).  Se viene rilevato un tag &quot;cue-in&quot; prima della fine di un’interruzione pubblicitaria, Adobe Primetime Ad Insertion rispetterà il cue-in.  Contatta il tuo Content Packager per abilitare la restituzione anticipata.
