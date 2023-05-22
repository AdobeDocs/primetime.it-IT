---
description: TVSDK per iOS include diverse funzioni.
title: Funzioni di Primetime TVSDK
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Funzioni di Primetime TVSDK {#primetime-tvsdk-features}

TVSDK per iOS include diverse funzioni e fornisce le seguenti funzionalità principali:

* VOD e riproduzione live/lineare

   * Gestione della finestra di riproduzione, inclusi i metodi di riproduzione, arresto, pausa, ricerca e recupero della posizione della testina di riproduzione
   * Supporto per la riproduzione completa degli eventi
   * Sottotitoli codificati (608, WebVTT) e forme audio alternative per una maggiore accessibilità
   * Capacità DVR
   * Logica di bit rate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Abbonamento a tag non HLS e HLS
   * Supporto del failover del manifesto live

* Pubblicità

   * VPAID 2.0
   * Unione di annunci lato client

      * Inserimento semplice degli annunci, incluso il supporto per VAST/VMAP
      * Supporto di tag di cue personalizzati per gli annunci
      * Supporto per contrassegnare, sostituire ed eliminare annunci C3
      * Flusso di lavoro personalizzabile per l&#39;inserimento di contenuti/annunci, inclusa la segnalazione di sospensione attività

* Protezione dei contenuti

   * Accesso ai servizi correlati alla gestione dei diritti digitali (DRM)
   * Riproduzione di flussi HLS non crittografati o con Protected HTTP Live Streaming (PHLS)
   * Controllo dell&#39;output basato su risoluzione, basato su regole DRM

* Tracciamento di video e annunci

   * Tracciamento eventi QoS
   * Notifiche che consentono a TVSDK e all’applicazione di comunicare in modo asincrono sullo stato di video, annunci pubblicitari e altri elementi, e anche su tale attività di registro
   * Integrazione con Adobe Analytics e supporto heartbeat

* Registrazione

   * Debug logging
