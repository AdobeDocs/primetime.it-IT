---
seo-title: Flusso di lavoro DRM AAXS standard
title: Flusso di lavoro DRM AAXS standard
description: Flusso di lavoro DRM AAXS standard
seo-description: Flusso di lavoro DRM AAXS standard
uuid: b996eb2c-8e37-4a29-a972-e09c69d2461d
translation-type: tm+mt
source-git-commit: 17a492d30c65b1b5e12419f04afa0116654b99fc
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Flusso di lavoro DRM AAXS standard{#standard-aaxs-drm-workflow}

1. (Pacchetto) L’SDK Java AXS genera un CEK casuale.
1. (Pacchetto) CEK viene utilizzato per cifrare il contenuto.
1. (Pacchetto) Il CEK viene crittografato utilizzando la chiave pubblica del server licenze AAXS.
1. (Pacchetto) Il CEK crittografato viene inserito nei metadati DRM del contenuto.
1. Il dispositivo tenta di riprodurre il contenuto richiedendo una licenza dal server AXS.
1. (Licenza) Il server AAXS utilizza la propria chiave privata per decrittografare il CEK dai metadati.
1. (Licenza) Il server AXS rilascia al dispositivo una licenza che contiene il CEK.
