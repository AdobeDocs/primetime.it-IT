---
description: Puoi completare flussi di lavoro specifici per Digital Rights Management (DRM).
title: Digital Rights Management
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Digital Rights Management {#digital-rights-management}

Puoi completare flussi di lavoro specifici per Digital Rights Management (DRM).

Puoi ascoltare l’evento `AdobePSDK.DRMMetadataInfoEvent` per gestire i flussi di lavoro DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Aggiungi Digital Rights Management {#add-digital-rights-management}

1. Aggiungi il `DRMMetadataInfoAvailableEvent` per ottenere il `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implementa la sezione `onDRMMetadataInfoAvailable` sopra la riga nel passaggio 1.

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

1. Crea il DRMManager nel metodo setupVideo .

   ```js
   var drmManager = player.drmManager;
   ```

1. Crea i dati di protezione per Widevine e PlayReady copiando il seguente esempio:

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

1. Modifica l’URL della risorsa in un flusso di test DASH.

   >[!TIP]
   >
   >Assicurati di aggiornare il tipo di risorsa, perché ora è DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Verifica la configurazione.