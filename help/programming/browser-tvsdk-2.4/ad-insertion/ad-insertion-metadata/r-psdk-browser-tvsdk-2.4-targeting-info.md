---
description: In Adobe Primetime ad Decioning puoi eseguire il targeting degli annunci su coppie chiave-valore.
title: Informazioni di targeting
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Informazioni di targeting{#targeting-information}

In Adobe Primetime ad Decioning puoi eseguire il targeting degli annunci su coppie chiave-valore.

Per trasmettere queste coppie di valori chiave al browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

