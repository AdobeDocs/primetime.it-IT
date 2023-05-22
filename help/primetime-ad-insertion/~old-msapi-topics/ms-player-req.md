---
description: Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e abilitare il tracciamento degli annunci.
title: Requisiti del lettore video
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Requisiti del lettore video {#video-player-requirements}

Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e abilitare il tracciamento degli annunci.

Per utilizzare l’API di inserimento annunci di Primetime, un lettore video deve soddisfare i seguenti requisiti:

* Può tenere traccia della posizione della testina di riproduzione durante la riproduzione del contenuto.
* Può richiedere gli URL di tracciamento nei tempi specificati.
* Viene eseguito su una piattaforma di dispositivi che supporta HLS v3 o versione successiva, tra cui:

   * Discontinuità PTS contrassegnate da `EXT-X-DISCONTINUITY` tag
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* Viene eseguito su una piattaforma che supporta i reindirizzamenti HTTP e l’analisi del codice JSON.
* Viene eseguito su una piattaforma che supporta CORS.