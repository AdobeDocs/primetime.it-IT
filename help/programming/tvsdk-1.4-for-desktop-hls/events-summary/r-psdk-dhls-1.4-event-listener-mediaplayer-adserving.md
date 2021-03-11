---
description: TVSDK invia eventi di ad-serving in risposta a operazioni con metadati temporizzati.
title: Eventi di trasmissione/metadati temporizzati degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Eventi di metadati relativi ad annunci/temporizzati{#ad-serving-timed-metadata-events}

TVSDK invia eventi di ad-serving in risposta a operazioni con metadati temporizzati.

Per ricevere notifiche su tutti gli eventi correlati, registra gli ascoltatori di eventi con l&#39;oggetto `MediaPlayer` per gli eventi seguenti.

| Evento | Significato |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Sono stati elaborati metadati temporizzati ID3. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | I metadati temporizzati sono stati elaborati e non è stata rilevata alcuna opportunità. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | I metadati temporizzati sono disponibili e non è stata rilevata alcuna opportunità. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | I metadati temporizzati sono stati elaborati e non è stata rilevata alcuna opportunità nel manifesto in background. |