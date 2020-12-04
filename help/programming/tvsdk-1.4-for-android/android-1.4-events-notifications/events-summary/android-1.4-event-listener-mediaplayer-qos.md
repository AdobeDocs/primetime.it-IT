---
description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.
seo-description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.
seo-title: Eventi QoS
title: Eventi QoS
uuid: 27f60cd3-d3fc-4ea3-81df-96d0fe9f7068
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Eventi QoS{#qos-events}

TVSDK invia eventi di qualità del servizio (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.

Per ricevere una notifica su tutti gli eventi relativi a QoS, registrare un&#39;implementazione di `MediaPlayer.QOSEventListener` che include le seguenti callback:

| Evento | Significato |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Buffering completato. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Buffering avviato. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | Download di un frammento completato. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification). [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) Avvertimento) | Si è verificato un errore reversibile. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustTime) | La ricerca è completa. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | La ricerca sta iniziando. |