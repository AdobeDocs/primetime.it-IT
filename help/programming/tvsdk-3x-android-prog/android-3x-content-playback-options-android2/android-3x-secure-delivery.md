---
description: TVSDK introduce la distribuzione protetta tramite HTTPS.
seo-description: TVSDK introduce la distribuzione protetta tramite HTTPS.
seo-title: Consegna protetta tramite HTTPS
title: Consegna protetta tramite HTTPS
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Consegna protetta tramite HTTPS {#secure-delivery-https}

 Adobe Primetime TVSDK fornisce il supporto per la consegna HTTPS per tutte le chiamate provenienti da TVSDK, che includono

* Chiamate al server Auditude Ad
* Richieste CRS
* Chiamate di licenza DRM
* Ping per analisi video
* Fissaggio

Per utilizzare questa funzione, accertatevi che i server configurati per la trasmissione delle richieste di cui sopra supportino HTTPS.

Per impostazione predefinita, questo nuovo comportamento non è attivato. Utilizzate quanto segue per abilitare la consegna protetta prima della chiamata a `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
