---
description: TVSDK introduce la consegna sicura tramite HTTPS.
title: Consegna sicura tramite HTTPS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Consegna sicura tramite HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK fornisce il supporto per la consegna HTTPS per tutte le chiamate provenienti da TVSDK, che includono

* Auditude delle chiamate ad server
* Richieste CRS
* Chiamate di licenza DRM
* Ping di analisi video
* Ping fatturazione

Per utilizzare questa funzione, assicurati che i server configurati per soddisfare le richieste di cui sopra supportino HTTPS.

Questo nuovo comportamento non è abilitato per impostazione predefinita. Utilizza quanto segue per abilitare la consegna sicura prima della chiamata a `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
