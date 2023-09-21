---
title: Flusso di lavoro DRM AAXS standard
description: Flusso di lavoro DRM AAXS standard
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Flusso di lavoro DRM AAXS standard{#standard-aaxs-drm-workflow}

1. (Pacchetto) L’SDK Java AAXS genera un CEK casuale.
1. (Pacchetto) Il codice CEK viene utilizzato per crittografare il contenuto.
1. (Pacchetto) Il codice CEK viene crittografato utilizzando la chiave pubblica del server licenze AAXS.
1. (Pacchetto) Il codice CEK crittografato viene inserito nei metadati DRM del contenuto.
1. Il dispositivo tenta di riprodurre il contenuto richiedendo una licenza dal server AAXS.
1. (Licenze) Il server AAXS utilizza la propria chiave privata per decrittografare il CEK dai metadati.
1. (Licenze) Il server AAXS rilascia al dispositivo una licenza che contiene il codice CEK.
