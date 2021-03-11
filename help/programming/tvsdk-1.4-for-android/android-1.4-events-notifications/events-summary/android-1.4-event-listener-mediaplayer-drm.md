---
description: TVSDK invia eventi di gestione dei diritti digitali (DRM) in risposta a operazioni relative a DRM, come quando nuovi metadati DRM diventano disponibili.
title: Eventi DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 1%

---


# Eventi DRM{#drm-events}

TVSDK invia eventi di gestione dei diritti digitali (DRM) in risposta a operazioni relative a DRM, come quando nuovi metadati DRM diventano disponibili.

Per ricevere notifiche su tutti gli eventi relativi a DRM, registra un&#39;implementazione di `MediaPlayer.DRMEventListener` che include il seguente callback.

| Evento | Significato |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Sono disponibili nuovi metadati DRM. |

