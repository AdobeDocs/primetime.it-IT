---
title: Anteprima licenza
description: Anteprima licenza
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Anteprima licenza {#license-preview}

Se si pone la questione se un dispositivo possa utilizzare o meno una licenza DRM Primetime e applicarla completamente, è possibile utilizzare la funzione Anteprima licenza. Una licenza di anteprima corrisponde completamente a tutti i vincoli e le restrizioni definiti nella licenza finale, ma non contiene la chiave di crittografia del contenuto (CEK) necessaria per decrittografare il contenuto protetto. Questa funzionalità è utile per determinare se il cliente può effettivamente utilizzare la licenza prima che il distributore di contenuti prenda la decisione di fornire una particolare licenza al cliente. Ad esempio: un cliente vuole guardare contenuti HD, ma il distributore dei contenuti vuole assicurarsi che il dispositivo possa rilevare e coinvolgere completamente l&#39;HDCP. In questa situazione, il client può chiamare `DRMManager.loadPreviewVoucher()`. Se un `DRMStatusEvent` è stato ricevuto, invece di un `DRMErrorEvent`, quindi viene confermato che il client può applicare completamente le restrizioni di protezione dell&#39;output nella licenza e che il distributore di contenuti può fornire liberamente questo tipo di licenza al client.

[AcquisisciLicenzaAnteprima iOS:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
