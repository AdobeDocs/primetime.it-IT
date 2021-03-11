---
description: TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che si incontrano tag predefiniti o personalizzati o quando una playlist cambia in un manifesto. Gli eventi vengono inviati nell'ordine in cui compaiono nel manifesto.
title: Eventi di metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Eventi metadati temporizzati{#timed-metadata-events}

TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che si incontrano tag predefiniti o personalizzati o quando una playlist cambia in un manifesto. Gli eventi vengono inviati nell&#39;ordine in cui compaiono nel manifesto.

Il lettore implementa azioni basate sui seguenti eventi:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Inviato quando sono stati elaborati i metadati temporizzati ID3.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Inviato quando i metadati temporizzati sono stati elaborati e non è stata rilevata alcuna opportunità.

