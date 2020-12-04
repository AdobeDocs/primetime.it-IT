---
description: Browser TVSDK fornisce le metriche da utilizzare per l'analisi e il debug. Potete ottenere queste metriche utilizzando QoSProvider.
seo-description: Browser TVSDK fornisce le metriche da utilizzare per l'analisi e il debug. Potete ottenere queste metriche utilizzando QoSProvider.
seo-title: Metriche
title: Metriche
uuid: 4734e532-1f83-4691-b1bd-785f78e55d8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 3%

---


# Metriche{#metrics}

Browser TVSDK fornisce le metriche da utilizzare per l&#39;analisi e il debug. Potete ottenere queste metriche utilizzando QoSProvider.

Ad esempio:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

