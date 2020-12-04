---
description: 'Sono state introdotte nuove API che indicheranno a TVSDK di ignorare lo stato di connettività di rete durante il download dei manifesti. '
seo-description: 'Sono state introdotte nuove API che indicheranno a TVSDK di ignorare lo stato di connettività di rete durante il download dei manifesti. '
seo-title: Riproduzione offline con Android
title: Riproduzione offline con Android
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Riproduzione offline con Android {#offline-playback-with-android}

Sono state introdotte le seguenti API che indicheranno a TVSDK di ignorare lo stato di connettività di rete durante il download dei manifesti. Lo stato di connettività di rete viene generalmente utilizzato durante lo streaming ABR (Adaptive Bitrate Streaming), per determinare se tentare un fallback o aspettare che la rete riprenda.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

È possibile abilitare questa impostazione e ignorare la connettività di rete.

Impostate `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` su true. Il valore predefinito per un valore booleano è false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
