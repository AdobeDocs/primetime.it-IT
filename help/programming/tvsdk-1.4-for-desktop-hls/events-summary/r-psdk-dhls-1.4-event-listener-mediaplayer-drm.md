---
description: TVSDK invia eventi di gestione dei diritti digitali (DRM) in risposta a operazioni relative a DRM, come quando nuovi metadati DRM diventano disponibili.
title: Eventi DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---


# Eventi DRM{#drm-events}

TVSDK invia eventi di gestione dei diritti digitali (DRM) in risposta a operazioni relative a DRM, come quando nuovi metadati DRM diventano disponibili.

Per ricevere notifiche su tutti gli eventi relativi a DRM, ascolta `DRMMetadataInfoEvent` per gli eventi DRM con l’oggetto `MediaPlayer` .

| Evento | Significato |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Sono disponibili nuovi metadati DRM. |