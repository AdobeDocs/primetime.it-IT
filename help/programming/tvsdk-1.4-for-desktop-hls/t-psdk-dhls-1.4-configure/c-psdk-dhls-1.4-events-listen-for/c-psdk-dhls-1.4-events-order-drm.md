---
description: TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare delle azioni in risposta a questi eventi.
seo-description: TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare delle azioni in risposta a questi eventi.
seo-title: Eventi DRM
title: Eventi DRM
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Eventi DRM{#drm-events}

TVSDK invia eventi DRM (Digital Rights Management) in risposta a operazioni DRM correlate, ad esempio quando diventano disponibili nuovi metadati DRM. Il lettore può implementare delle azioni in risposta a questi eventi.

Per ricevere notifiche su tutti gli eventi relativi a DRM, ascolta quanto segue:

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

