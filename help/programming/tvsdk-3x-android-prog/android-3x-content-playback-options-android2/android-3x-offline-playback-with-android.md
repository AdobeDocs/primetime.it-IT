---
description: Sono state introdotte nuove API che indicheranno a TVSDK di ignorare lo stato della connettività di rete durante il download dei manifesti.
title: Riproduzione offline con Android
exl-id: 9ac50d3e-5839-4eb9-8811-efde56cfe375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Riproduzione offline con Android {#offline-playback-with-android}

Sono state introdotte le seguenti API che indicheranno a TVSDK di ignorare lo stato della connettività di rete durante il download dei manifesti. Lo stato di connettività di rete viene generalmente utilizzato durante il flusso di bitrate adattivo (ABR, Adaptive Bitrate Streaming) per determinare se tentare un fallback o attendere la ripresa della rete.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

È possibile abilitare questa impostazione e ignorare la connettività di rete.

Imposta `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` su true. Il valore predefinito per un valore booleano è false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
