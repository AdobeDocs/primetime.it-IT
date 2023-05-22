---
title: Concatenamento licenze
description: Concatenamento licenze
copied-description: true
exl-id: 2f439e21-c748-45aa-a87c-36e70ee3722a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Concatenamento licenze{#license-chaining}

Se il criterio utilizzato per generare la licenza supporta il concatenamento delle licenze, il server deve decidere se rilasciare una licenza Leaf, una licenza Root o entrambe. Per determinare il tipo di concatenamento delle licenze supportato da un criterio, utilizzare `Policy.getLicenseChainType()`, o chiama `Policy.getRootLicenseId()` per determinare se il criterio dispone di una licenza root. Con il concatenamento delle licenze di Adobe Access 2.0, in genere il server rilascia una licenza foglia la prima volta che l&#39;utente richiede una licenza per un determinato computer e successivamente una licenza root. Per determinare se il computer dispone già di una licenza foglia per il criterio specificato, chiamare `LicenseRequestMessage.clientHasLeafForPolicy()`.
