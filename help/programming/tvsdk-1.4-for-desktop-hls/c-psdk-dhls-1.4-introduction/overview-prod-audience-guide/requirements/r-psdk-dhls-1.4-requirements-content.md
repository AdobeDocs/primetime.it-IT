---
description: Controlla le limitazioni e i requisiti per flussi e playlist (manifesti), comprese le chiavi di crittografia DRM.
seo-description: Controlla le limitazioni e i requisiti per flussi e playlist (manifesti), comprese le chiavi di crittografia DRM.
seo-title: Requisiti di contenuto e manifesto
title: Requisiti di contenuto e manifesto
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Requisiti di contenuto e manifesto {#content-and-manifest-requirements}

Controlla le limitazioni e i requisiti per flussi e playlist (manifesti), comprese le chiavi di crittografia DRM.

| Includere e impostare la `RESOLUTION` proprietà per ciascun flusso ABR nel file manifesto. È necessario utilizzare Flash Player 14 o versione successiva. |
|---|
| Se il flusso protetto da DRM è a bitrate multiplo (MBR), la chiave di crittografia DRM utilizzata per l&#39;MBR deve essere la stessa utilizzata per tutti i flussi di bitrate. |
| Devono avere le stesse rappresentazioni bitrate delle rappresentazioni del contenuto principale. |