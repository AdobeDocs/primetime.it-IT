---
description: TVSDK supporta l’eliminazione programmatica e la sostituzione del contenuto degli annunci nei flussi VOD.
title: Operazioni con intervalli di tempo personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Panoramica {#custom-time-range-operations-overview}

TVSDK supporta l’eliminazione programmatica e la sostituzione del contenuto degli annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione degli ad markers personalizzati. Gli ad markers personalizzati contrassegnano sezioni del contenuto principale come periodi di contenuto relativi agli annunci. Oltre a contrassegnare questi intervalli di tempo, puoi anche eliminare e sostituire gli intervalli di tempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

L’eliminazione e la sostituzione degli annunci sono implementate con marcatori personalizzati che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegna, elimina e sostituisci. Per ogni intervallo di tempo personalizzato, puoi eseguire le operazioni associate, inclusa l’eliminazione o la sostituzione del contenuto dell’annuncio.

Per l&#39;eliminazione e la sostituzione degli annunci, TVSDK include le seguenti modalità *funzionamento dell&#39;intervallo di tempo personalizzato*:

* MARK - Invia eventi `AdBreak` per le aree contrassegnate. (Questa funzione era denominata `customAdMarker` nelle versioni precedenti di TVSDK.) Inserimento di annunci non consentito in questa modalità.

* DELETE: per questa modalità, l’app utilizza la classe `TimeRangeCollection` per definire le aree di tempo per l’eliminazione di annunci C3. L’inserimento di annunci è consentito in questa modalità.
* SOSTITUISCI : in questa modalità, l&#39;app sostituisce un `timeRange` con un ad decision ioning Adobe Primetime `AdBreak`. L&#39;operazione di sostituzione inizia dove si verifica l&#39;eliminazione dell&#39;annuncio C3 e termina all&#39;ora indicata (più breve o più lungo dell&#39;intervallo di tempo originale).

TVSDK fornisce una classe `CustomRangesOpportunityGenerator` per generare opportunità di posizionamento per gli intervalli MARK e DELETE. Per la modalità REPLACE, TVSDK genera due opportunità di posizionamento per ogni intervallo di tempo:

* `CustomRangeResolver` genera opportunità di posizionamento per DELETE
* Il `AuditudeAdResolver` genera opportunità di posizionamento per INSERT.