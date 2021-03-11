---
description: Il browser TVSDK invia eventi di qualità del servizio (QoS) per notificare all’applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e ricerca.
title: Eventi QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Eventi QoS{#qos-events}

Il browser TVSDK invia eventi di qualità del servizio (QoS) per notificare all’applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e ricerca.

Per ricevere notifiche su tutti gli eventi relativi a QoS, crea un&#39;istanza di `AdobePSDK.QOSProvider` e allega l&#39;istanza MediaPlayer a questa istanza `QOSProvider`:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configura un timer nell&#39;applicazione per controllare periodicamente la proprietà `playbackInformation` dell&#39;istanza `qosProvider`. La proprietà `playbackInformation` fornisce un&#39;istantanea delle statistiche di riproduzione correnti. Ad esempio:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

