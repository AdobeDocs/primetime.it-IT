---
description: Il TVSDK del browser fornisce metriche da utilizzare per l’analisi e il debug. Puoi ottenere queste metriche utilizzando QoSProvider.
title: Metriche
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Metriche{#metrics}

Il TVSDK del browser fornisce metriche da utilizzare per l’analisi e il debug. Puoi ottenere queste metriche utilizzando QoSProvider.

Ad esempio:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
