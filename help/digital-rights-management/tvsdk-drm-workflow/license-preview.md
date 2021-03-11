---
title: Anteprima della licenza
description: Anteprima della licenza
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Anteprima licenza {#license-preview}

Se c&#39;è una domanda se un dispositivo può utilizzare o meno una licenza DRM di Primetime e applicare completamente una licenza DRM di Primetime, è possibile utilizzare la funzione Anteprima licenza. Una licenza di anteprima corrisponde completamente a tutti i vincoli e le restrizioni definiti nella licenza finale, ma non contiene la chiave di crittografia del contenuto (CEK) necessaria per decrittografare il contenuto protetto. Questa funzionalità è utile per determinare se il cliente può effettivamente utilizzare la licenza prima che il distributore di contenuti prenda una decisione per fornire una licenza specifica al cliente. Ad esempio, un cliente desidera guardare i contenuti HD, ma il distributore dei contenuti vuole assicurarsi che il dispositivo possa rilevare e coinvolgere completamente HDCP. In questa situazione, il client può chiamare `DRMManager.loadPreviewVoucher()`. Se viene ricevuto un `DRMStatusEvent` invece di un `DRMErrorEvent`, viene confermato che il client può applicare pienamente le restrizioni di protezione dell&#39;output contenute nella licenza e che il distributore di contenuti può liberamente fornire questo tipo di licenza al cliente.

[AcquisizionePreviewLicense per iOS:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
