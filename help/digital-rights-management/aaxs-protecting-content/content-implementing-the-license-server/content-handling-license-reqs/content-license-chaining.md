---
seo-title: Concatenamento delle licenze
title: Concatenamento delle licenze
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Concatenamento delle licenze{#license-chaining}

Se il criterio utilizzato per generare la licenza supporta il concatenamento delle licenze, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambi. Per determinare il tipo di licenza che il concatenamento di un criterio supporta, utilizzate `Policy.getLicenseChainType()`o chiamate `Policy.getRootLicenseId()` per determinare se il criterio dispone di una licenza radice. Con il concatenamento delle licenze di Adobe Access 2.0, il server in genere rilascia una licenza foglia la prima volta che l&#39;utente richiede una licenza per un particolare computer e una licenza root in seguito. Per determinare se il computer dispone già di una licenza foglia per il criterio specificato, chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.
