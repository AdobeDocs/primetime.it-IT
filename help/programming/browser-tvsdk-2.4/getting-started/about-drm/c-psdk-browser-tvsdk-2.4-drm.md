---
description: Potete completare flussi di lavoro specifici per Digital Rights Management (DRM).
seo-description: Potete completare flussi di lavoro specifici per Digital Rights Management (DRM).
seo-title: Digital Rights Management
title: Digital Rights Management
uuid: 011605c7-50c4-4ad5-9961-8cd92d0e6fd8
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Digital Rights Management {#digital-rights-management}

Potete completare flussi di lavoro specifici per Digital Rights Management (DRM).

Potete ascoltare l&#39;evento `AdobePSDK.DRMMetadataInfoEvent` per gestire i flussi di lavoro DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Aggiungi Digital Rights Management {#add-digital-rights-management}

1. Aggiungete il simbolo `DRMMetadataInfoAvailableEvent` per ottenere il simbolo `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implementare la sezione `onDRMMetadataInfoAvailable` sopra la riga al punto 1.

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. Create DRMManager nel metodo setupVideo.

   ```js
   var drmManager = player.drmManager;
   ```

1. Create i dati di protezione per Widevine e PlayReady copiando il seguente esempio:

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. Aggiungi i dati di protezione a drmManager.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. Modificate l’URL della risorsa in un flusso di prova DASH.

   >[!TIP]
   >
   >Assicurarsi di aggiornare il tipo di risorsa, perché ora è DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Verificate la configurazione.