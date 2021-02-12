---
description: Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e per abilitare il tracciamento degli annunci.
seo-description: Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e per abilitare il tracciamento degli annunci.
seo-title: Requisiti del lettore video
title: Requisiti del lettore video
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '138'
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
* I lettori basati su Web devono essere eseguiti su piattaforme che supportano CORS.