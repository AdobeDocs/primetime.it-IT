---
description: TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che si incontrano tag predefiniti o personalizzati o quando una playlist cambia in un manifesto. Gli eventi vengono inviati nell’ordine in cui appaiono nel manifest.
seo-description: TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che si incontrano tag predefiniti o personalizzati o quando una playlist cambia in un manifesto. Gli eventi vengono inviati nell’ordine in cui appaiono nel manifest.
seo-title: Eventi di metadati temporizzati
title: Eventi di metadati temporizzati
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Eventi metadati temporizzati{#timed-metadata-events}

TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che si incontrano tag predefiniti o personalizzati o quando una playlist cambia in un manifesto. Gli eventi vengono inviati nell’ordine in cui appaiono nel manifest.

Il lettore implementa le azioni in base ai seguenti eventi:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Inviato quando vengono elaborati metadati ID3 temporizzati.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Inviato quando i metadati temporizzati venivano elaborati e non veniva rilevata alcuna opportunità.

