---
description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all’applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.
title: Eventi QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Eventi QoS{#qos-events}

TVSDK invia eventi di qualità del servizio (QoS) per notificare all’applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.

Per ricevere notifiche su tutti gli eventi relativi a QoS, registra gli ascoltatori di eventi con l&#39;oggetto `MediaPlayer` per i seguenti eventi:

| Evento | Significato |
|---|---|
| BufferEvent.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | Buffering completato. |
| BufferEvent.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | Buffering avviato. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | Ricerca completata. |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | La ricerca sta iniziando. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK ha modificato la posizione di ricerca a seguito dei criteri pubblicitari correnti. |

