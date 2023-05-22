---
title: Concatenamento licenze migliorato
description: Concatenamento licenze migliorato
copied-description: true
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Concatenamento licenze migliorato {#enhanced-license-chaining}

Se si utilizza un criterio DRM per generare una licenza che supporta il concatenamento delle licenze, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambe. Se si desidera determinare il tipo di concatenamento delle licenze supportato da un criterio DRM, è necessario utilizzare `Policy.getLicenseChainType()`, o chiama `Policy.getRootLicenseId()` per determinare se il criterio DRM dispone di una licenza radice. Con il concatenamento delle licenze di Adobe Primetime DRM 2.0, il server in genere rilascia una licenza foglia la prima volta che un utente richiede una licenza per un determinato computer e successivamente una licenza root. Se si desidera determinare se il computer dispone già di una licenza foglia per il criterio specificato, è necessario chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.

Con il concatenamento delle licenze migliorato in Adobe Primetime DRM 3.0, si consiglia di rilasciare sia un Leaf che un Root la prima volta che l’utente richiede una licenza per una particolare macchina. Se l’utente dispone già della licenza Root, il server può emettere solo un Leaf (chiamata `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` per determinare se il client dispone già di una radice avanzata 3.0). Per le richieste di licenza successive, il client indica quindi di disporre già di una licenza Leaf e di una licenza Root, pertanto il server deve rilasciare una nuova licenza Root. Quando si utilizza il concatenamento avanzato delle licenze, `setRootKeyRetrievalInfo()` è necessario chiamare per fornire le credenziali necessarie per decrittografare la chiave di crittografia radice nel criterio DRM.

>[!NOTE]
>
>Se la policy supporta il concatenamento delle licenze avanzato 3.0, ma il client è Primetime DRM 2.0, il server rilascia una licenza concatenata originale 2.0. Per determinare la versione del client, utilizza `LicenseRequestMessage.getClientVersion()`.
