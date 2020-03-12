---
description: TVSDK invia eventi di trasmissione di annunci in risposta a operazioni di metadati temporizzate.
seo-description: TVSDK invia eventi di trasmissione di annunci in risposta a operazioni di metadati temporizzate.
seo-title: Eventi di trasmissione/visualizzazione di metadati temporizzati
title: Eventi di trasmissione/visualizzazione di metadati temporizzati
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventi di trasmissione/visualizzazione di metadati temporizzati{#ad-serving-timed-metadata-events}

TVSDK invia eventi di trasmissione di annunci in risposta a operazioni di metadati temporizzate.

Per ricevere notifiche su tutti questi eventi correlati, registrare i listener di eventi con l&#39; `MediaPlayer` oggetto per gli eventi seguenti.

| Evento | Significato |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Sono stati elaborati metadati ID3 temporizzati. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | I metadati temporizzati sono stati elaborati e non è stata rilevata alcuna opportunità. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | I metadati temporizzati sono disponibili e non è stata rilevata alcuna opportunità. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | I metadati temporizzati sono stati elaborati e non è stata rilevata alcuna opportunità nel manifesto in background. |