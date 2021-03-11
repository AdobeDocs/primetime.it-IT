---
title: Concatena delle licenze migliorata
description: Concatena delle licenze migliorata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Concatena delle licenze migliorata {#enhanced-license-chaining}

Se si utilizza un criterio DRM per generare una licenza che supporta il concatenamento delle licenze, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambe. Se desideri determinare il tipo di licenza supportata dal concatenamento di una policy DRM, devi utilizzare `Policy.getLicenseChainType()` o chiamare `Policy.getRootLicenseId()` per determinare se il criterio DRM dispone di una licenza radice. Con la catena di licenze Adobe Primetime DRM 2.0, il server in genere rilascia una licenza foglia la prima volta che un utente richiede una licenza per un particolare computer e una licenza root in seguito. Per determinare se il computer dispone già di una licenza foglia per il criterio specificato, è necessario chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.

Con una catena di licenze migliorata in Adobe Primetime DRM 3.0, si consiglia di emettere sia una foglia che una radice la prima volta che l&#39;utente richiede una licenza per un particolare computer. Se l&#39;utente dispone già della licenza Root, il server può emettere solo una chiamata Leaf (chiamare `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` per determinare se il client dispone già di una radice Enhanced 3.0). Per le richieste di licenza successive, il client indica quindi che dispone già di una foglia e di una radice, pertanto il server dovrebbe rilasciare una nuova licenza Root. Quando si utilizza il concatenamento di licenze avanzato, `setRootKeyRetrievalInfo()` deve essere chiamato per fornire le credenziali necessarie per decrittografare la chiave di crittografia radice nel criterio DRM.

>[!NOTE]
>
>Se il criterio supporta la catena di licenze ottimizzata 3.0, ma il client è Primetime DRM 2.0, il server rilascia una licenza a catena originale 2.0. Per determinare la versione client, utilizza `LicenseRequestMessage.getClientVersion()`.

