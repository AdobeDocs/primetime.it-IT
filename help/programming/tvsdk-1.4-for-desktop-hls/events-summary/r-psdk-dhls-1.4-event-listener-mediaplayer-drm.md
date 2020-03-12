---
description: TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM.
seo-description: TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM.
seo-title: Eventi DRM
title: Eventi DRM
uuid: f1da5b31-3fad-4bb4-8aa3-3925d5f0e123
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventi DRM{#drm-events}

TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM.

Per ricevere notifiche su tutti gli eventi relativi a DRM, ascoltare `DRMMetadataInfoEvent` gli eventi DRM con l&#39; `MediaPlayer` oggetto.

| Evento | Significato |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Sono disponibili nuovi metadati DRM. |