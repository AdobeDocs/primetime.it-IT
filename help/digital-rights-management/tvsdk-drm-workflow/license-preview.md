---
seo-title: Anteprima licenza
title: Anteprima licenza
uuid: 61ff171f-b977-40ef-8e8d-2900316fa89a
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Anteprima licenza {#license-preview}

In caso di dubbi sulla possibilità o meno di utilizzare un dispositivo per applicare completamente una licenza DRM di Primetime, potete utilizzare la funzione Anteprima licenza. Una licenza di anteprima soddisfa completamente tutti i vincoli e le restrizioni definiti nella licenza finale, ma non contiene la chiave di crittografia dei contenuti (CEK) necessaria per decifrare il contenuto protetto. Questa funzionalità è utile per determinare se il cliente può effettivamente utilizzare la licenza prima che il distributore dei contenuti decida di fornire una licenza particolare al cliente. Ad esempio, un cliente desidera guardare i contenuti HD, ma il distributore dei contenuti vuole assicurarsi che il dispositivo sia in grado di rilevare e coinvolgere completamente HDCP. In questa situazione, il client può chiamare `DRMManager.loadPreviewVoucher()`. Se viene ricevuto un `DRMStatusEvent`, invece di un `DRMErrorEvent`, viene confermato che il client può applicare completamente le restrizioni di Protezione output contenute nella licenza e che il distributore di contenuti può liberamente fornire questo tipo di licenza al client.

[AcquisizionePreviewLicense per iOS:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
