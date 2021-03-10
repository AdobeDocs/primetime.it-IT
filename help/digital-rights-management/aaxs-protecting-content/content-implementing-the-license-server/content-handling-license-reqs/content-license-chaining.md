---
title: Concatenamento delle licenze
description: Concatenamento delle licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Concatena di licenze{#license-chaining}

Se il criterio utilizzato per generare la licenza supporta il concatenamento delle licenze, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambi. Per determinare il tipo di licenza supportata dal concatenamento di un criterio, utilizza `Policy.getLicenseChainType()` o chiama `Policy.getRootLicenseId()` per determinare se il criterio dispone di una licenza radice. Con la catena di licenze di Adobe Access 2.0, in genere il server rilascia una licenza foglia la prima volta che l&#39;utente richiede una licenza per un particolare computer e una licenza root in seguito. Per determinare se il computer dispone già di una licenza foglia per il criterio specificato, chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.
