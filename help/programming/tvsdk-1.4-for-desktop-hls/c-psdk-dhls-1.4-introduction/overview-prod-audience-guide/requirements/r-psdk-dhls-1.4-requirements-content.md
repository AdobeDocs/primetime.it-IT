---
description: Controlla le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.
title: Requisiti relativi al contenuto e al manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Requisiti relativi al contenuto e al manifesto {#content-and-manifest-requirements}

Controlla le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| Includi e imposta la proprietà `RESOLUTION` per ogni flusso ABR nel file manifesto. È necessario utilizzare il Flash Player 14 o versione successiva. |
|---|
| Se il flusso protetto da DRM è a bit rate multiplo (MBR), la chiave di crittografia DRM utilizzata per l&#39;MBR deve essere la stessa della chiave utilizzata in tutti i flussi a bit rate. |
| Deve avere le stesse rappresentazioni a bit rate delle rappresentazioni del contenuto principale. |