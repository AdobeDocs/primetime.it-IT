---
description: In Adobe Primetime ad un processo decisionale per gli annunci, puoi eseguire il targeting degli annunci su coppie chiave-valore.
seo-description: In Adobe Primetime ad un processo decisionale per gli annunci, puoi eseguire il targeting degli annunci su coppie chiave-valore.
seo-title: Informazioni sul targeting
title: Informazioni sul targeting
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Informazioni sul targeting{#targeting-information}

In Adobe Primetime ad un processo decisionale per gli annunci, puoi eseguire il targeting degli annunci su coppie chiave-valore.

Per trasmettere queste coppie di valori chiave a Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

