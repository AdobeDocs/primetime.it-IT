---
description: Puoi implementare più soluzioni DRM per le tue app TVSDK utilizzando Primetime DRM Cloud, con tecnologia ExpressPlay. Le soluzioni DRM includono Apple FairPlay, Google Widevine, Microsoft PlayReady e Primetime Access dall'Adobe.
title: Panoramica su più DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Flussi di lavoro multi-DRM {#multi-drm-workflows}

Puoi implementare più soluzioni DRM per le tue app TVSDK utilizzando Primetime DRM Cloud, con tecnologia ExpressPlay. Le soluzioni DRM includono Apple FairPlay, Google Widevine, Microsoft PlayReady e Primetime Access dall&#39;Adobe.

## Panoramica di Multi-DRM {#multi-drm-overview}

Adobe TVSDK supporta la protezione DRM utilizzando più schemi DRM. Adobe offre *Primetime DRM Cloud, con tecnologia ExpressPlay* per fornire packaging, licenze e riproduzione di contenuti video su più piattaforme.

Gli schemi DRM supportati includono Adobe *Primetime Access* DRM (AAXS), così come DRM nativi su vari dispositivi, tra cui [Widevine](https://www.widevine.com) su Chrome e Android, [FairPlay](https://developer.apple.com/streaming/fps/) su Safari e iOS e [PlayReady](https://www.microsoft.com/playready/) su e XboxOne. Consulta un rappresentante di Adobe per informazioni sugli schemi DRM attualmente disponibili su queste piattaforme, nonché sulle date pianificate delle versioni future.

TVSDK supporta le licenze DRM rilasciate da qualsiasi server di licenze che utilizza questi protocolli. Oltre al supporto per più soluzioni DRM, Adobe offre *Primetime DRM Cloud, con tecnologia ExpressPlay* come soluzione in cui ExpressPlay gestisce i server di licenza per ciascuna soluzione. Questo può semplificare la configurazione e la manutenzione per le tue esigenze di rilascio della licenza DRM.

Per utilizzare *Primetime DRM Cloud, basato su ExpressPlay* per implementare le tue esigenze DRM nelle app TVSDK, devi prima ottenere un account [ExpressPlay.com](https://www.expressplay.com). ExpressPlay fornisce la capacità di licenza per diversi schemi di protezione DRM e fornisce anche altri servizi, tra cui la gestione di pacchetti e chiavi.

Il tuo rappresentante Adobe configurerà inizialmente il tuo account ExpressPlay. Puoi quindi configurare il tuo account e ottenere gli *autenticatori cliente* che utilizzerai nelle richieste di token di licenza per i server ExpressPlay.