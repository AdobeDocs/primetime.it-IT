---
description: Tutti i lettori video devono fornire funzionalità su cui il server manifest si basa per inserire annunci e per abilitare il tracciamento degli annunci.
title: Requisiti del lettore video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Requisiti del lettore video {#video-player-requirements}

Tutti i lettori video devono fornire funzionalità su cui il server manifest si basa per inserire annunci e per abilitare il tracciamento degli annunci.

Per utilizzare l&#39;API di inserimento annunci Primetime, un lettore video deve soddisfare i seguenti requisiti:

* Può tenere traccia della posizione della testina di riproduzione durante la riproduzione del contenuto.
* Può richiedere gli URL di tracciamento nei momenti specificati.
* Viene eseguito su una piattaforma di dispositivi che supporta HLS v3 o versioni successive, tra cui:

   * Discontinuità PTS contrassegnata dai tag `EXT-X-DISCONTINUITY`
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Viene eseguito su una piattaforma che supporta i reindirizzamenti HTTP e l’analisi di JSON.
* I lettori basati sul web devono essere eseguiti su piattaforme che supportano CORS.