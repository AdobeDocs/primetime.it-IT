---
description: Tutti i lettori video devono fornire funzionalità su cui il server manifesto si basa per inserire annunci e abilitare il tracciamento degli annunci.
title: Requisiti del lettore video
exl-id: 23134e4c-6902-4b97-bf15-4524f47850e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
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
* I lettori basati su web devono essere eseguiti su piattaforme che supportano CORS.
