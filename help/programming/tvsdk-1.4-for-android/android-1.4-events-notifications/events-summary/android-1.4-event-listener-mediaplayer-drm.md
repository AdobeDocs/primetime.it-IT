---
description: TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM.
title: Eventi DRM
exl-id: 8a3bd8c7-1e76-4d26-8f88-e29eb0a0e1b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Eventi DRM{#drm-events}

TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM.

Per ricevere notifiche su tutti gli eventi relativi a DRM, registrare un&#39;implementazione di `MediaPlayer.DRMEventListener` che include il seguente callback.

| Evento | Significato |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Sono disponibili nuovi metadati DRM. |
