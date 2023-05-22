---
description: In Adobe Primetime ad decisioning puoi eseguire il targeting degli annunci su coppie chiave-valore.
title: Informazioni di targeting
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
