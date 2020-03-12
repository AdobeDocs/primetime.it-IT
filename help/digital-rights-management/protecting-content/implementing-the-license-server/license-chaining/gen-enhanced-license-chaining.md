---
seo-title: Concatenamento Delle Licenze Migliorato
title: Concatenamento Delle Licenze Migliorato
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Concatenamento Delle Licenze Migliorato {#enhanced-license-chaining}

Se per generare una licenza che supporti il concatenamento delle licenze viene utilizzato un criterio DRM, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambi. Se si desidera determinare il tipo di concatenamento di licenze supportato da un criterio DRM, è necessario utilizzare `Policy.getLicenseChainType()`, o chiamare, `Policy.getRootLicenseId()` per determinare se il criterio DRM dispone di una licenza radice. Con il concatenamento delle licenze Adobe Primetime DRM 2.0, il server in genere rilascia una licenza foglia la prima volta che un utente richiede una licenza per un particolare computer e una licenza root in seguito. Se si desidera determinare se il computer dispone già di una licenza foglia per il criterio specificato, è necessario chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.

Con la concatenazione delle licenze avanzata in Adobe Primetime DRM 3.0, si consiglia di rilasciare sia una foglia che una radice la prima volta che l&#39;utente richiede una licenza per un particolare computer. Se l&#39;utente dispone già della licenza Root, il server può emettere solo una chiamata Leaf (per determinare se il client dispone già di una radice Enhanced 3.0). `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` Per le richieste di licenza successive, il client indica che dispone già di una foglia e di una radice, pertanto il server dovrebbe emettere una nuova licenza Root. Quando si utilizza il concatenamento delle licenze avanzato, `setRootKeyRetrievalInfo()` deve essere chiamato per fornire le credenziali necessarie per decifrare la chiave di crittografia radice nel criterio DRM.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Se il criterio supporta il concatenamento delle licenze avanzato 3.0, ma il client è Primetime DRM 2.0, il server rilascia quindi una licenza concatenata originale 2.0. Per determinare la versione client, utilizzate `LicenseRequestMessage.getClientVersion()`.

