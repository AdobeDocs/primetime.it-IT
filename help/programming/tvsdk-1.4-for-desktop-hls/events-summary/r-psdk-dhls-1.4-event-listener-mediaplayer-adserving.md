---
description: TVSDK invia eventi ad-serving in risposta a operazioni di metadati a tempo.
title: Eventi di metadati ad serving/temporizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Eventi di metadati ad serving/temporizzati{#ad-serving-timed-metadata-events}

TVSDK invia eventi ad-serving in risposta a operazioni di metadati a tempo.

Per ricevere notifiche su tutti gli eventi correlati, registra i listener di eventi con `MediaPlayer` per i seguenti eventi.

| Evento | Significato |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Metadati temporizzati ID3 elaborati. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Metadati temporizzati elaborati. Nessuna opportunità rilevata. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | I metadati temporizzati sono disponibili e non è stata rilevata alcuna opportunità. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Metadati temporizzati elaborati. Nessuna opportunità rilevata nel manifesto in background. |
