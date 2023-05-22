---
description: TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che vengono rilevati tag predefiniti o personalizzati o quando una playlist viene modificata in un manifesto. Gli eventi vengono inviati nell’ordine in cui compaiono nel manifesto.
title: Eventi metadati temporizzati
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Eventi metadati temporizzati{#timed-metadata-events}

TVSDK invia eventi di metadati temporizzati e genera metadati temporizzati ogni volta che vengono rilevati tag predefiniti o personalizzati o quando una playlist viene modificata in un manifesto. Gli eventi vengono inviati nell’ordine in cui compaiono nel manifesto.

Il lettore implementa azioni basate sui seguenti eventi:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: inviato quando è stato elaborato un metadati con tempistica ID3.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: inviato quando sono stati elaborati i metadati temporizzati e non è stata rilevata alcuna opportunità.
