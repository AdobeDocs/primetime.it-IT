---
description: TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare azioni in risposta a questi eventi.
title: Eventi DRM
exl-id: 712347f3-f103-4c08-ad19-af1dd59ac549
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Eventi DRM{#drm-events}

TVSDK invia eventi DRM (Digital Rights Management) in risposta alle operazioni relative a DRM, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare azioni in risposta a questi eventi.

Per ricevere notifiche su tutti gli eventi relativi a DRM, attendere quanto segue:

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

L’esempio seguente mostra una progressione tipica:

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```
