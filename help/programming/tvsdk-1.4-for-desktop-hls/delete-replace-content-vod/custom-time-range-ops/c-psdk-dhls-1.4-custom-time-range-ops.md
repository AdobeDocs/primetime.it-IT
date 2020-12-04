---
description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.
seo-description: TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.
seo-title: Operazioni intervallo di tempo personalizzato
title: Operazioni intervallo di tempo personalizzato
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Panoramica {#custom-time-range-operations-overview}

TVSDK supporta l’eliminazione e la sostituzione programmatica del contenuto degli annunci nei flussi VOD.

La funzione di eliminazione e sostituzione estende la funzione degli indicatori di annunci personalizzati. I marcatori annunci personalizzati contrassegnano sezioni del contenuto principale come periodi di contenuto correlati agli annunci. Oltre a contrassegnare questi intervalli di tempo, potete anche eliminare e sostituire gli intervalli di tempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

L’eliminazione e la sostituzione degli annunci sono implementate con marcatori personalizzati che identificano diversi tipi di intervalli di tempo in un flusso VOD: contrassegnare, eliminare e sostituire. Per ciascun intervallo di tempo personalizzato, potete eseguire le operazioni associate, compresa l&#39;eliminazione o la sostituzione del contenuto di un annuncio.

Per l&#39;eliminazione e la sostituzione degli annunci, TVSDK include le seguenti modalità *per l&#39;utilizzo dell&#39;intervallo di tempo personalizzato*:

* MARK - Invia eventi `AdBreak` per le aree contrassegnate. (Questa funzione era denominata `customAdMarker` nelle versioni precedenti di TVSDK.) L&#39;inserimento di annunci non è consentito in questa modalità.

* DELETE - Per questa modalità, l&#39;app utilizza la classe `TimeRangeCollection` per definire le aree temporali per l&#39;eliminazione di annunci C3. L&#39;inserimento di annunci è consentito in questa modalità.
* SOSTITUISCI - In questa modalità, l&#39;app sostituisce un `timeRange` con un  Adobe Primetime con un annuncio `AdBreak`. L&#39;operazione di sostituzione inizia nel punto in cui si verifica l&#39;eliminazione di C3 Ad e termina all&#39;ora indicata (più breve o più lunga dell&#39;intervallo di tempo originale).

TVSDK fornisce una classe `CustomRangesOpportunityGenerator` per generare opportunità di posizionamento per gli intervalli MARK e DELETE. Per la modalità REPLACE, TVSDK genera due opportunità di posizionamento per ogni intervallo di tempo:

* `CustomRangeResolver` genera opportunità di posizionamento per i DELETE
* La `AuditudeAdResolver` genera opportunità di posizionamento per INSERT.