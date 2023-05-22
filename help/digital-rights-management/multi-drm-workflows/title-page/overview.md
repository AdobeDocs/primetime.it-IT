---
description: Puoi implementare più soluzioni DRM per le app TVSDK utilizzando Primetime DRM Cloud, con tecnologia ExpressPlay. Le soluzioni DRM includono FairPlay di Apple, Widevine di Google, PlayReady di Microsoft e Primetime Access di Adobe.
title: Panoramica di Multi-DRM
exl-id: 27614bb6-bfa6-445a-8fb5-a1b8af080bcc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Flussi di lavoro multi-DRM {#multi-drm-workflows}

Puoi implementare più soluzioni DRM per le app TVSDK utilizzando Primetime DRM Cloud, con tecnologia ExpressPlay. Le soluzioni DRM includono FairPlay di Apple, Widevine di Google, PlayReady di Microsoft e Primetime Access di Adobe.

## Panoramica di Multi-DRM {#multi-drm-overview}

Adobe TVSDK supporta la protezione DRM utilizzando più schemi DRM. Adobe di offerte *Primetime DRM Cloud, con tecnologia ExpressPlay* per fornire pacchetti, licenze e riproduzione dei contenuti video su più piattaforme.

Gli schemi DRM supportati includono Adobe *Accesso Primetime* DRM (AAXS) e DRM nativi su vari dispositivi, tra cui [Widevine](https://www.widevine.com) su Chrome e Android, [FairPlay](https://developer.apple.com/streaming/fps/) su Safari e iOS, e [PlayReady](https://www.microsoft.com/playready/) su Edge e Xbox One. Consultate un rappresentante di Adobi per informazioni sugli schemi DRM attualmente disponibili su queste piattaforme e sulle date previste per le versioni future.

TVSDK supporta le licenze DRM rilasciate da qualsiasi server di licenze che utilizza questi protocolli. Oltre al supporto per più soluzioni DRM, Adobe offre *Primetime DRM Cloud, con tecnologia ExpressPlay* come soluzione in cui ExpressPlay gestisce i server di licenze per ciascuna soluzione. Questo consente di semplificare la configurazione e la manutenzione per le esigenze di rilascio delle licenze DRM.

Da utilizzare *Primetime DRM Cloud, con tecnologia ExpressPlay* per implementare le tue esigenze DRM nelle app TVSDK, devi prima ottenere un’ [ExpressPlay.com](https://www.expressplay.com) account. ExpressPlay offre la possibilità di concedere licenze per diversi schemi di protezione DRM e offre anche altri servizi, tra cui la gestione di pacchetti e chiavi.

Il rappresentante di Adobe configurerà inizialmente l&#39;account ExpressPlay. Puoi quindi configurare il tuo account e ottenere il *autenticatori cliente* che utilizzerai nelle richieste di token di licenza per i server ExpressPlay.
