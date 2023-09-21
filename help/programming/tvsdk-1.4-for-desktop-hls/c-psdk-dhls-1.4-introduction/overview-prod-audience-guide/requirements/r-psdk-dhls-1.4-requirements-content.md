---
description: Controllare le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.
title: Requisiti del contenuto e del manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Requisiti del contenuto e del manifesto {#content-and-manifest-requirements}

Controllare le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| Includi e imposta `RESOLUTION` per ogni flusso ABR nel file manifesto. Deve usare il Flash Player 14 o successivo. |
|---|
| Se il flusso protetto da DRM è a velocità bit multipla (MBR), la chiave di crittografia DRM utilizzata per l&#39;MBR deve essere la stessa della chiave utilizzata in tutti i flussi di velocità bit. |
| Deve avere le stesse rappresentazioni a bit rate delle rappresentazioni del contenuto principale. |
