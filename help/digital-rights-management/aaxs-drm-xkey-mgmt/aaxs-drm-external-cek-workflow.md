---
seo-title: Flusso di lavoro CEK esterno DRM AAXS
title: Flusso di lavoro CEK esterno DRM AAXS
description: Questo flusso di lavoro si discosta dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l'utilizzo di repository centrale o di Content Key Management System (CKMS)
seo-description: Questo flusso di lavoro si discosta dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l'utilizzo di repository centrale o di Content Key Management System (CKMS)
uuid: b313594b-0feb-4f27-bf02-f04b955e2140
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc

---


# Flusso di lavoro CEK esterno DRM AAXS{#aaxs-drm-external-cek-workflow}

Questo flusso di lavoro si discosta dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l&#39;utilizzo di repository centrale o di Content Key Management System (CKMS). Tuttavia, per i clienti che desiderano che AAXS lavori con il CKMS esistente, AAXS fornisce una funzione chiamata &quot;Esterno CEK&quot;, in cui il CEK viene fornito esternamente al momento del rilascio della confezione e della licenza.

![](assets/ECEK_Workflow.PNG)

1. (Pacchetto) L’SDK Java AXS viene fornito con un CEK e un ID CEK.
1. (Pacchetto) CEK viene utilizzato per cifrare il contenuto.
1. (Pacchetto) L&#39;ID CEK viene inserito nei metadati DRM del contenuto.
1. Il dispositivo tenta di riprodurre il contenuto richiedendo una licenza dal server AXS.
1. (Licenza) Il server AXS estrae l’ID CEK dai metadati del contenuto.
1. Il server AAXS recupera il CEK dal CKMS.
1. (Licenza) Il server AXS rilascia al dispositivo una licenza che contiene il CEK.
