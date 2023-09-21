---
description: TVSDK invia eventi Quality of Service (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come il buffering o la ricerca.
title: Eventi QoS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Eventi QoS{#qos-events}

TVSDK invia eventi Quality of Service (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come il buffering o la ricerca.

Per ricevere notifiche su tutti gli eventi relativi al QoS, registra i listener di eventi con `MediaPlayer` oggetto per i seguenti eventi:

| Evento | Significato |
|---|---|
| BufferEvent.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | Buffering completato. |
| BufferEvent.[INIZIO_BUFFERING](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | Buffering avviato. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | Ricerca completata. |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | Inizio della ricerca. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK ha cambiato la posizione di ricerca a seguito delle attuali politiche pubblicitarie. |
