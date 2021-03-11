---
description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all’applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.
title: Eventi QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Eventi QoS{#qos-events}

TVSDK invia eventi di qualità del servizio (QoS) per notificare all’applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.

Per ricevere notifiche su tutti gli eventi relativi a QoS, registra un&#39;implementazione di `MediaPlayer.QOSEventListener` che include i seguenti callback:

| Evento | Significato |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Buffering completato. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Buffering avviato. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo)) (loadInfo) | Download di un frammento completato. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html) (MediaPlayerNotification). [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) Avviso) | Errore recuperabile. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long)) (long fixed time) | Ricerca completata. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | La ricerca sta iniziando. |