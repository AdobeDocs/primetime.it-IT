---
description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.
seo-description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.
seo-title: Eventi QoS
title: Eventi QoS
uuid: fd657cf0-c6d4-4e9a-b212-7d09d483cae9
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventi QoS{#qos-events}

TVSDK invia eventi di qualità del servizio (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio buffering o ricerca.

Per ricevere notifiche su tutti gli eventi relativi a QoS, registrare i listener di eventi con l&#39; `MediaPlayer` oggetto per gli eventi seguenti:

| Evento | Significato |
|---|---|
| BufferEvent.[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | Buffering completato. |
| BufferEvent.[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | Buffering avviato. |
| SeekEvent.[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | La ricerca è completa. |
| SeekEvent.[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | La ricerca sta iniziando. |
| SeekEvent.[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK ha modificato la posizione di ricerca come risultato delle politiche pubblicitarie correnti. |

