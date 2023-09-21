---
description: TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che vengono rilevati tag predefiniti o personalizzati o quando una playlist viene modificata in un manifesto. Gli eventi vengono inviati nell’ordine in cui compaiono nel manifesto.
title: Eventi metadati temporizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Eventi metadati temporizzati{#timed-metadata-events}

TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che vengono rilevati tag predefiniti o personalizzati o quando una playlist viene modificata in un manifesto. Gli eventi vengono inviati nell’ordine in cui compaiono nel manifesto.

Il lettore implementa azioni basate sui seguenti eventi:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: inviato quando è stato elaborato un metadati con tempistica ID3.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: inviato quando sono stati elaborati i metadati temporizzati e non è stata rilevata alcuna opportunità.
