---
title: Server di licenza DRM di Primetime
description: Server di licenza DRM di Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Server di licenze DRM Primetime {#primetime-drm-license-server}

Il server di licenza DRM di Primetime è costruito dall&#39;SDK Java DRM di Primetime. Questo server utilizza le richieste di licenza dei client che richiedono l’accesso al contenuto protetto. Il server è in grado di analizzare e manipolare i criteri DRM dall&#39;interno della richiesta di licenza, al fine di modificare o sostituire il criterio prima di utilizzare il criterio per generare una licenza per il client richiedente.

Per implementare un server di licenza DRM di Primetime, deve prima soddisfare **le regole di conformità e robustezza di Adobe** per DRM di Primetime. Adobe offre anche un servizio di licenze DRM in hosting Primetime chiamato [Primetime Cloud DRM](../cloud-quick-start/whats-included.md), che puoi utilizzare come alternativa all&#39;hosting del tuo server di licenze.
