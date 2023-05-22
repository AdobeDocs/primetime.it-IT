---
description: Controllare le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.
title: Requisiti del contenuto e del manifesto
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
