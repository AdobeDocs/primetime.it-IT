---
title: Flusso di lavoro DRM AXS standard
description: Flusso di lavoro DRM AXS standard
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Flusso di lavoro DRM AXS standard{#standard-aaxs-drm-workflow}

1. (Pacchetto) L&#39;SDK Java AAXS genera un CEK casuale.
1. (Pacchetto) La CEK viene utilizzata per crittografare il contenuto.
1. (Pacchetto) La CEK viene crittografata utilizzando la chiave pubblica del server licenze AAXS.
1. (Pacchetto) Il CEK crittografato viene inserito nei metadati DRM del contenuto.
1. Il dispositivo tenta di riprodurre il contenuto richiedendo una licenza dal server AXS.
1. (Licenze) Il server AAXS utilizza la propria chiave privata per decrittografare la CEK dai metadati.
1. (Licenze) Il server AAXS rilascia al dispositivo una licenza che contiene il CEK.
