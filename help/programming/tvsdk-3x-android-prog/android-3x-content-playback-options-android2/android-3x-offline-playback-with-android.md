---
description: Sono state introdotte nuove API che indicheranno a TVSDK di ignorare lo stato della connettività di rete durante il download dei manifesti.
title: Riproduzione offline con Android
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
