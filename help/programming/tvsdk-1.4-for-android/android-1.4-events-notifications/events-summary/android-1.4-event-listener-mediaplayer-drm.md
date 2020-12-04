---
description: TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM.
seo-description: TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM.
seo-title: Eventi DRM
title: Eventi DRM
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Eventi DRM{#drm-events}

TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM.

Per ricevere notifiche su tutti gli eventi relativi a DRM, registrare un&#39;implementazione di `MediaPlayer.DRMEventListener` che include il callback seguente.

| Evento | Significato |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Sono disponibili nuovi metadati DRM. |

