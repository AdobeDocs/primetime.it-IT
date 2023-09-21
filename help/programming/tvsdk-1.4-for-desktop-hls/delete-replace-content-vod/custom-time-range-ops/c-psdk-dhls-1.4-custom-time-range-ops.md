---
description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto di annunci nei flussi VOD.
title: Operazioni per intervalli di tempo personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Panoramica {#custom-time-range-operations-overview}

TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto di annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione dei marcatori di annunci personalizzati. I marcatori di annunci personalizzati contrassegnano le sezioni del contenuto principale come periodi di contenuto relativi agli annunci. Oltre a contrassegnare questi intervalli di tempo, puoi anche eliminarli e sostituirli.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

L’eliminazione e la sostituzione degli annunci vengono implementate con marcatori personalizzati che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegna, elimina e sostituisci. Per ogni intervallo di tempo personalizzato, puoi eseguire le operazioni associate, inclusa l’eliminazione o la sostituzione del contenuto dell’annuncio.

Per l’eliminazione e la sostituzione degli annunci, TVSDK include quanto segue *operazione intervallo di tempo personalizzato* modalità:

* MARK - Dispatches `AdBreak` eventi per le regioni contrassegnate. (Chiamato `customAdMarker` nelle versioni precedenti di TVSDK.) L’inserimento di annunci non è consentito in questa modalità.

* DELETE: per questa modalità, l’app utilizza `TimeRangeCollection` per definire le aree temporali per l&#39;eliminazione dell&#39;annuncio C3. L’inserimento di annunci è consentito in questa modalità.
* REPLACE - In questa modalità, l’app sostituisce un `timeRange` con Adobe Primetime ad decisioning `AdBreak`. L’operazione di sostituzione inizia nel punto in cui si verifica l’eliminazione dell’annuncio C3 e termina all’ora indicata (più breve o più lunga dell’intervallo di tempo originale).

TVSDK fornisce un `CustomRangesOpportunityGenerator` per generare opportunità di posizionamento per gli intervalli MARK e DELETE. Per la modalità SOSTITUISCI, TVSDK genera due opportunità di posizionamento per ogni intervallo di tempo:

* Il `CustomRangeResolver` genera opportunità di posizionamento per DELETE
* Il `AuditudeAdResolver` genera opportunità di posizionamento per INSERT.
