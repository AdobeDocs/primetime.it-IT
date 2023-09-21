---
title: Flusso di lavoro CEK esterno AAXS DRM
description: Questo flusso di lavoro rappresenta un allontanamento dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l'utilizzo di alcun archivio centrale o sistema di gestione delle chiavi di contenuto (Content Key Management System, CKMS)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Flusso di lavoro CEK esterno AAXS DRM{#aaxs-drm-external-cek-workflow}

Questo flusso di lavoro rappresenta un allontanamento dalla maggior parte dei sistemi DRM esistenti, in quanto non richiede l&#39;utilizzo di alcun archivio centrale o sistema di gestione delle chiavi di contenuto (Content Key Management System, CKMS). Tuttavia, per i clienti che desiderano che AAXS lavori con le loro CKMS esistenti, AAXS fornisce una funzione chiamata &quot;External CEK&quot;, in cui il CEK viene fornito esternamente al momento dell&#39;imballaggio e del rilascio della licenza.

![](assets/ECEK_Workflow.PNG)

1. (Pacchetto) L’SDK Java di AAXS è dotato di un CEK e un ID CEK.
1. (Pacchetto) Il codice CEK viene utilizzato per crittografare il contenuto.
1. (Pacchetto) L’ID di verifica viene inserito nei metadati DRM del contenuto.
1. Il dispositivo tenta di riprodurre il contenuto richiedendo una licenza dal server AAXS.
1. (Licenze) Il server AAXS estrae l’ID CEK dai metadati del contenuto.
1. Il server AAXS recupera il CEK dal CKMS.
1. (Licenze) Il server AAXS rilascia al dispositivo una licenza che contiene il codice CEK.
