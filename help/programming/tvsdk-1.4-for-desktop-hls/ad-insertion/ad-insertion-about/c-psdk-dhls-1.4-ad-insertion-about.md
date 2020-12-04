---
description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
seo-description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
seo-title: Inserimento di annunci
title: Inserimento di annunci
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Panoramica {#inserting-ads-overview}

L&#39;inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.

Un *`ad break`* contiene uno o più annunci che vengono riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

## Disattiva annunci pre-roll {#disable-preroll-ads}

Per disattivare il pre-roll, modificate i generatori di opportunità predefiniti in modo da non effettuare la chiamata pre-roll. I generatori di opportunità predefiniti sono:

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

Per disattivare il pre-roll sui flussi live, modificare quanto sopra in modo da includere solo SpliceOutOpportunityGenerator:

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
