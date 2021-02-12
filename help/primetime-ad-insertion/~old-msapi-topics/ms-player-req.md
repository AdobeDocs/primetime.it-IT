---
description: Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e per abilitare il tracciamento degli annunci.
seo-description: Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e per abilitare il tracciamento degli annunci.
seo-title: Requisiti del lettore video
title: Requisiti del lettore video
uuid: 29593d67-2901-4d9e-a08f-23c8a7667283
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Requisiti del lettore video {#video-player-requirements}

Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e per abilitare il tracciamento degli annunci.

Per utilizzare l’API di inserimento degli annunci Primetime, un lettore video deve soddisfare i requisiti seguenti:

* Può tenere traccia della posizione dell&#39;indicatore di riproduzione durante la riproduzione del contenuto.
* Può richiedere gli URL di tracciamento nei momenti specificati.
* Viene eseguito su una piattaforma di dispositivi che supporta HLS v3 o versione successiva, inclusi:

   * Discontinuità PTS contrassegnata dai tag `EXT-X-DISCONTINUITY`
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Viene eseguito su una piattaforma che supporta i reindirizzamenti HTTP e l&#39;analisi di JSON.
* Viene eseguito su una piattaforma che supporta CORS.