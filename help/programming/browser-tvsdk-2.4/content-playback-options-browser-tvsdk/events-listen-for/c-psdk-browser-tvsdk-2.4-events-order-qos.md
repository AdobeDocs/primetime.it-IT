---
description: Il browser TVSDK invia eventi Quality of Service (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come ad esempio gli eventi di buffering e ricerca.
title: Eventi QoS
exl-id: b0fab68e-ef0f-4812-b4ad-3f69dcdf2d9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Eventi QoS{#qos-events}

Il browser TVSDK invia eventi Quality of Service (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come ad esempio gli eventi di buffering e ricerca.

Per ricevere notifiche su tutti gli eventi correlati al QoS, crea un’istanza di `AdobePSDK.QOSProvider` e allega l&#39;istanza MediaPlayer a questo `QOSProvider` istanza:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configurare un timer nell&#39;applicazione per controllare periodicamente `playbackInformation` proprietà del `qosProvider` dell&#39;istanza. Il `playbackInformation` fornisce un’istantanea delle statistiche di riproduzione correnti. Ad esempio:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
