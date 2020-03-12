---
seo-title: Generazione di licenze
title: Generazione di licenze
uuid: f91b0cc8-e0ed-4722-947b-22eb2bfba916
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Generazione di licenze{#generating-licenses}

Se desiderate rilasciare una licenza foglia a un utente, l’SDK deve decifrare il CEK contenuto nei metadati del contenuto e crittografarlo nuovamente per il computer che richiede una licenza. Per decrittografare la CEK, il server deve fornire le informazioni necessarie per decifrare la chiave. Chiamare `ContentInfo.setKeyRetrievalInfo()` e fornire un `AsymmetricKeyRetrieval` oggetto. Se i metadati includono più criteri, il server deve determinare quali criteri utilizzare e chiamare `LicenseRequestMessage.setSelectedPolicy()`. Quindi chiama `LicenseRequestMessage.generateLicense()` per generare la licenza. Utilizzando l&#39; `License` oggetto restituito, è possibile modificare la scadenza o i diritti nella licenza.

Se un `ExternalKeyRetrieval` oggetto è specificato nell&#39; `ContentInfo` oggetto, il server licenze deve utilizzare l&#39;ID CEK associato per recuperare il CEK appropriato inserito nella licenza.

Per ulteriori informazioni sull’utilizzo del flusso di lavoro CEK esterno, consulta Panoramica [di](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) Adobe Primetime DRM DRM Esterno.
