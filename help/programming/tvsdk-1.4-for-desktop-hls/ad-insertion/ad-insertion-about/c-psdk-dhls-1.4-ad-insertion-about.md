---
description: L’inserimento di annunci risolve gli annunci per video on-demand (VOD) , per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.
title: Inserimento annunci
exl-id: 3a472435-2e37-46d6-8c08-dd6e953c7a7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Panoramica {#inserting-ads-overview}

L’inserimento di annunci risolve gli annunci per video on-demand (VOD) , per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.

Un *`ad break`* contiene uno o più annunci riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

## Disattiva annunci pre-roll {#disable-preroll-ads}

Per disabilitare il pre-roll, modifica i generatori di opportunità predefiniti in modo da non effettuare la chiamata pre-roll. I generatori di opportunità predefiniti sono:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

Per disabilitare il pre-roll sui flussi live, modifica quanto sopra in modo da includere solo SpliceOutOpportunityGenerator:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```
