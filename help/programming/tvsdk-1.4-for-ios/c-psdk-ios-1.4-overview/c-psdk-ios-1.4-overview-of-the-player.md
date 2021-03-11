---
description: TVSDK per iOS include numerose funzioni.
title: Funzioni TVSDK di Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Funzioni TVSDK di Primetime {#primetime-tvsdk-features}

TVSDK per iOS include numerose funzioni e fornisce le seguenti funzionalità principali:

* Riproduzione VOD e live/lineare

   * Gestione della finestra di riproduzione, compresi i metodi che riproducono, fermano, mettono in pausa, cercano e recuperano la posizione della testina di riproduzione
   * Supporto per la riproduzione a eventi completi
   * Sottotitoli codificati (608, WebVTT) e moduli audio alternativi per una maggiore accessibilità
   * Funzionalità DVR
   * Logica del bit rate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Iscrizione a tag non HLS e HLS
   * Supporto del failover del manifesto in tempo reale

* Pubblicità

   * VPAID 2.0
   * Unione di annunci lato client

      * Inserimento senza problemi di annunci, compreso il supporto per VAST/VMAP
      * Supporto per tag cue personalizzati per gli annunci
      * Supporto per la marcatura, la sostituzione e l’eliminazione degli annunci C3
      * Flusso di lavoro di inserimento di contenuti/annunci personalizzabili, inclusa la segnaletica di blackout

* Protezione dei contenuti

   * Accesso ai servizi relativi alla gestione dei diritti digitali (DRM)
   * Riproduzione di flussi HLS non crittografati o con HTTP Live Streaming (PHLS) protetto
   * Controllo dell&#39;uscita basato su risoluzione, basato su criteri DRM

* Tracciamento video e annunci

   * Tracciamento degli eventi QoS
   * Notifiche che aiutano TVSDK e la tua applicazione a comunicare in modo asincrono lo stato dei video, degli annunci pubblicitari e di altri elementi, nonché l’attività di log
   * Integrazione con Adobe Analytics e supporto heartbeat

* Registrazione

   * Debug logging

