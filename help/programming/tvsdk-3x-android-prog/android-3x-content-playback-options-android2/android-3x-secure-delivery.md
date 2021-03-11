---
description: TVSDK introduce una consegna sicura su HTTPS.
title: Consegna sicura tramite HTTPS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Consegna sicura tramite HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK fornisce il supporto per la consegna HTTPS per tutte le chiamate provenienti da TVSDK, che includono

* Chiamate al server di annunci audio
* Richieste CRS
* Chiamate di licenza DRM
* Pings di Video Analytics
* Pali di fatturazione

Per utilizzare questa funzione, assicurati che i server configurati per il servizio delle richieste di cui sopra supportino HTTPS.

Questo nuovo comportamento non è abilitato per impostazione predefinita. Utilizza quanto segue per abilitare la consegna sicura prima della chiamata a `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
