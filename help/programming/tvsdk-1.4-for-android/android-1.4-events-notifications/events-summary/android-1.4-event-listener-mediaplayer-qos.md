---
description: TVSDK invia eventi Quality of Service (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come il buffering o la ricerca.
title: Eventi QoS
exl-id: 0ccdaed1-1fce-46b7-b0f0-25e7ea98da86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Eventi QoS{#qos-events}

TVSDK invia eventi Quality of Service (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come il buffering o la ricerca.

Per ricevere notifiche su tutti gli eventi relativi al QoS, registra un’implementazione di `MediaPlayer.QOSEventListener` inclusi i seguenti callback:

| Evento | Significato |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Buffering completato. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Buffering avviato. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | Un frammento è stato scaricato correttamente. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification. [Avvertenza](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) avvertenza) | Si è verificato un errore irreversibile. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustTime) | Ricerca completata. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | Inizio della ricerca. |
