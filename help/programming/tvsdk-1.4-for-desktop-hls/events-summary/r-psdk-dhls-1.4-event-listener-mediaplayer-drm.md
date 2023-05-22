---
description: TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM.
title: Eventi DRM
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Eventi DRM{#drm-events}

TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM.

Per ricevere notifiche su tutti gli eventi relativi a DRM, attendere `DRMMetadataInfoEvent` per gli eventi DRM con `MediaPlayer` oggetto.

| Evento | Significato |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Sono disponibili nuovi metadati DRM. |
