---
description: Potete implementare più soluzioni DRM per le vostre app TVSDK utilizzando Primetime DRM Cloud, basato su ExpressPlay. Le soluzioni DRM includono Apple FairPlay, Google Widevine, Microsoft PlayReady e Primetime Access dal Adobe .
seo-description: Potete implementare più soluzioni DRM per le vostre app TVSDK utilizzando Primetime DRM Cloud, basato su ExpressPlay. Le soluzioni DRM includono Apple FairPlay, Google Widevine, Microsoft PlayReady e Primetime Access dal Adobe .
seo-title: Panoramica di Multi-DRM
title: Panoramica di Multi-DRM
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# Flussi di lavoro multi-DRM {#multi-drm-workflows}

Potete implementare più soluzioni DRM per le vostre app TVSDK utilizzando Primetime DRM Cloud, basato su ExpressPlay. Le soluzioni DRM includono Apple FairPlay, Google Widevine, Microsoft PlayReady e Primetime Access dal Adobe .

## Panoramica multi-DRM {#multi-drm-overview}

 Adobe TVSDK supporta la protezione DRM utilizzando più schemi DRM.  Adobe offre *Primetime DRM Cloud, basato su ExpressPlay* per fornire pacchetti, licenze e riproduzione dei contenuti video su più piattaforme.

Gli schemi DRM supportati includono  Adobe  *Accesso Primetime* DRM (AAXS), nonché DRM nativi su vari dispositivi, tra cui [Widevine](https://www.widevine.com) su Chrome e Android, [FairPlay](https://developer.apple.com/streaming/fps/) su Safari e iOS e [PlayReady](https://www.microsoft.com/playready/) su e XboxOne. Consultate un rappresentante del Adobe  per informazioni sugli schemi DRM attualmente disponibili su queste piattaforme, nonché sulle date previste per le release future.

TVSDK supporta le licenze DRM rilasciate da qualsiasi server di licenze che utilizza questi protocolli. Oltre al supporto per più soluzioni DRM,  Adobe offre *Primetime DRM Cloud, basato su ExpressPlay* come soluzione in cui ExpressPlay gestisce i server delle licenze per ciascuna soluzione. Questo può semplificare la configurazione e la manutenzione per le esigenze di rilascio delle licenze DRM.

Per utilizzare *Primetime DRM Cloud, basato su ExpressPlay* per implementare le esigenze DRM nelle app TVSDK, è innanzitutto necessario ottenere un account [ExpressPlay.com](https://www.expressplay.com). ExpressPlay fornisce la capacità di licenza per diversi schemi di protezione DRM, e fornisce anche altri servizi, tra cui la gestione di pacchetti e chiavi.

Il rappresentante  Adobe configurerà inizialmente il tuo account ExpressPlay. Potete quindi configurare l&#39;account e ottenere gli *autenticatori cliente* che verranno utilizzati nelle richieste di token di licenza per i server ExpressPlay.