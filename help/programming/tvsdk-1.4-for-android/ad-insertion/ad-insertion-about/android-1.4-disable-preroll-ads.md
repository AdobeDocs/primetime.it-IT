---
title: Disattiva annunci pre-roll
description: Disattiva annunci pre-roll
copied-description: true
exl-id: ff52588e-540e-4072-bec0-e531c8cb6fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---

# Disattiva annunci pre-roll{#disable-pre-roll-ads}

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
