---
description: È possibile completare i flussi di lavoro specifici del Digital Rights Management (DRM).
title: Digital Rights Management
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

È possibile completare i flussi di lavoro specifici del Digital Rights Management (DRM).

È possibile ascoltare `AdobePSDK.DRMMetadataInfoEvent` evento per gestire i flussi di lavoro DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Aggiungi Digital Rights Management {#add-digital-rights-management}

1. Aggiungi il `DRMMetadataInfoAvailableEvent` per ottenere `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implementare `onDRMMetadataInfoAvailable` sopra la riga nel passaggio 1.

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

1. Creare DRMManager nel metodo setupVideo.

   ```js
   var drmManager = player.drmManager;
   ```

1. Creare i dati di protezione per Widevine e PlayReady copiando il seguente esempio:

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

1. Aggiungere i dati di protezione a drmManager.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. Modifica l’URL della risorsa in un flusso di test DASH.

   >[!TIP]
   >
   >Assicurati di aggiornare il tipo di risorsa, perché ora si tratta di DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Verifica la configurazione.
