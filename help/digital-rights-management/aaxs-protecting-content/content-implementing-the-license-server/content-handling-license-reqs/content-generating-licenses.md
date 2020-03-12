---
seo-title: Generazione di licenze
title: Generazione di licenze
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Generazione di licenze {#generating-licenses}

Per rilasciare una licenza foglia all’utente, l’SDK deve decifrare il CEK contenuto nei metadati del contenuto e crittografarlo nuovamente per il computer che richiede una licenza. Per decrittografare la CEK, il server deve fornire le informazioni necessarie per decifrare la chiave. Chiamare `ContentInfo.setKeyRetrievalInfo()` e fornire un `AsymmetricKeyRetrieval` oggetto. Se i metadati contengono più criteri, il server deve determinare quali criteri utilizzare e chiamare `LicenseRequestMessage.setSelectedPolicy()`. Quindi chiama `LicenseRequestMessage.generateLicense()` per generare la licenza. Utilizzando l&#39; `License` oggetto restituito, è possibile modificare la scadenza o i diritti nella licenza.

Se nell&#39; `ContentInfo` oggetto è specificato un oggetto ExternalKeyRetrieval, il server licenze deve utilizzare l&#39;ID CEK associato per recuperare il CEK appropriato che verrà inserito nella licenza. Per ulteriori dettagli sull&#39;utilizzo del flusso di lavoro CEK esterno, vedere Panoramica di [Adobe Access DRM External CEK](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
