---
description: 'Sono state introdotte nuove API che istruiranno a TVSDK di ignorare lo stato di connettività di rete durante il download dei manifesti. '
title: Riproduzione offline con Android
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Riproduzione offline con Android {#offline-playback-with-android}

Sono state introdotte le seguenti API che istruiranno a TVSDK di ignorare lo stato di connettività di rete durante il download dei manifesti. Lo stato di connettività di rete viene generalmente utilizzato durante lo streaming a bitrate adattivo (ABR), per determinare se tentare un fallback o attendere che la rete riprenda.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Puoi abilitare questa impostazione e ignorare la connettività di rete.

Imposta `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` su true. Il valore predefinito per un valore booleano è false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
