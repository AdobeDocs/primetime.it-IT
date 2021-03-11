---
description: Il browser TVSDK fornisce metriche da utilizzare per l’analisi e il debug. Puoi ottenere queste metriche utilizzando QoSProvider.
title: Metriche
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 5%

---


# Metriche{#metrics}

Il browser TVSDK fornisce metriche da utilizzare per l’analisi e il debug. Puoi ottenere queste metriche utilizzando QoSProvider.

Ad esempio:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

