---
description: TVSDK invia eventi di gestione dei diritti digitali (DRM) in risposta a operazioni relative a DRM, come quando nuovi metadati DRM diventano disponibili. Il lettore può implementare azioni in risposta a questi eventi.
title: Eventi DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Eventi DRM{#drm-events}

TVSDK invia eventi di gestione dei diritti digitali (DRM) in risposta a operazioni relative a DRM, come quando nuovi metadati DRM diventano disponibili. Il lettore può implementare azioni in risposta a questi eventi.

Per ricevere notifiche su tutti gli eventi relativi a DRM, tieni presente quanto segue:

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

