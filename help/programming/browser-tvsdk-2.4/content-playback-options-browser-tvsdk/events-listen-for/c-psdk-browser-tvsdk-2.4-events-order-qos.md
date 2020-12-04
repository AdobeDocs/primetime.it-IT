---
description: Browser TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e di ricerca.
seo-description: Browser TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e di ricerca.
seo-title: Eventi QoS
title: Eventi QoS
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# Eventi QoS{#qos-events}

Browser TVSDK invia eventi di qualità del servizio (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e di ricerca.

Per ricevere notifiche su tutti gli eventi relativi a QoS, create un&#39;istanza di `AdobePSDK.QOSProvider` e allegate l&#39;istanza MediaPlayer a questa istanza `QOSProvider`:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configurare un timer nell&#39;applicazione per controllare periodicamente la proprietà `playbackInformation` dell&#39;istanza `qosProvider`. La proprietà `playbackInformation` fornisce un&#39;istantanea delle statistiche di riproduzione correnti. Ad esempio:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

