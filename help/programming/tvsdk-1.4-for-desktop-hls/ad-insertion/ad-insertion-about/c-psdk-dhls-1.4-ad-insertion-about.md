---
description: L’inserimento di annunci risolve gli annunci per video-on-demand (VOD) , per streaming live e per streaming lineare con tracciamento degli annunci e riproduzione di annunci. TVSDK invia le richieste richieste al server di annunci, riceve le informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
title: Inserimento di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Panoramica {#inserting-ads-overview}

L’inserimento di annunci risolve gli annunci per video-on-demand (VOD) , per streaming live e per streaming lineare con tracciamento degli annunci e riproduzione di annunci. TVSDK invia le richieste richieste al server di annunci, riceve le informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.

Un *`ad break`* contiene uno o più annunci che vengono riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

## Disattiva gli annunci pre-roll {#disable-preroll-ads}

Per disattivare il pre-roll, modifica i generatori di opportunità predefiniti in modo da non effettuare la chiamata pre-roll. I generatori di opportunità predefiniti sono:

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

Per disabilitare il pre-roll sui flussi live, modifica quanto sopra in modo da includere solo il SpliceOutOpportunityGenerator:

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
