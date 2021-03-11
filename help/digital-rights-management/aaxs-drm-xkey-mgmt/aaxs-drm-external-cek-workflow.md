---
title: Flusso di lavoro CEK esterno DRM AXS
description: Questo flusso di lavoro si discosta dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l'utilizzo di repository centrale o Content Key Management System (CKMS)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Flusso di lavoro CEK esterno AAXS DRM{#aaxs-drm-external-cek-workflow}

Questo flusso di lavoro si discosta dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l’utilizzo di repository centrale o CKMS (Content Key Management System). Tuttavia, per i clienti che desiderano che AAXS lavori con i loro CKMS esistenti, AAXS fornisce una funzione chiamata &quot;Esterno CEK&quot;, in cui il CEK viene fornito esternamente al momento del rilascio delle confezioni e delle licenze.

![](assets/ECEK_Workflow.PNG)

1. (Pacchetto) L&#39;SDK Java AAXS viene fornito con un CEK e un ID CEK.
1. (Pacchetto) La CEK viene utilizzata per crittografare il contenuto.
1. (Pacchetto) L&#39;ID CEK viene inserito nei metadati DRM del contenuto.
1. Il dispositivo tenta di riprodurre il contenuto richiedendo una licenza dal server AXS.
1. (Licenza) Il server AAXS estrae l’ID CEK dai metadati del contenuto.
1. Il server AAXS recupera il CEK dal CKMS.
1. (Licenze) Il server AAXS rilascia al dispositivo una licenza che contiene il CEK.
