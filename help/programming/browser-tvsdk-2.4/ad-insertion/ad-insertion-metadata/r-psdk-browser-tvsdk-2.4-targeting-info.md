---
description: In Adobe Primetime ad decisioning puoi eseguire il targeting degli annunci su coppie chiave-valore.
title: Informazioni di targeting
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Informazioni di targeting{#targeting-information}

In Adobe Primetime ad decisioning puoi eseguire il targeting degli annunci su coppie chiave-valore.

Per passare queste coppie di valori chiave a Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
