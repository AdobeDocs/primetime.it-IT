---
title: Concatenamento licenze
description: Concatenamento licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Concatenamento licenze{#license-chaining}

Se il criterio utilizzato per generare la licenza supporta il concatenamento delle licenze, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambe. Per determinare il tipo di concatenamento delle licenze supportato da un criterio, utilizzare `Policy.getLicenseChainType()`, o chiama `Policy.getRootLicenseId()` per determinare se il criterio dispone di una licenza root. Con il concatenamento delle licenze di Adobe Access 2.0, in genere il server rilascia una licenza foglia la prima volta che l&#39;utente richiede una licenza per un determinato computer e successivamente una licenza root. Per determinare se il computer dispone già di una licenza foglia per il criterio specificato, chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.
