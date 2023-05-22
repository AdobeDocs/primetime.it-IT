---
description: TVSDK per Android include diverse funzioni e fornisce le seguenti funzionalità principali
title: Funzioni di Primetime TVSDK
exl-id: 7df03752-98aa-4317-8e41-a284472cabbb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Funzioni di Primetime TVSDK{#primetime-tvsdk-features}

TVSDK per Android include una serie di funzioni e fornisce le seguenti funzionalità principali:

* VOD e riproduzione live/lineare

   * Gestione della finestra di riproduzione, inclusi i metodi di riproduzione, arresto, pausa, ricerca e recupero della posizione della testina di riproduzione
   * Supporto per la riproduzione completa degli eventi
   * Sottotitoli codificati (608, 708, WebVTT) e forme alternative di audio per una maggiore accessibilità
   * Controllo per lo stile del testo nei sottotitoli
   * Capacità DVR, avanzamento rapido/riavvolgimento rapido (modalità di riproduzione con selezione)
   * Logica di bit rate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Supporto del failover del manifesto live
   * Buffer di riproduzione regolabili
   * Supporto del tracciamento per durata, dimensione e tempo di download dei frammenti

* Pubblicità

   * VPAID 2.0
   * Unione di annunci lato client

      * Inserimento parziale dell’interruzione pubblicitaria, che consente a un’esperienza simile a quella televisiva di essere in grado di unirsi nel mezzo di un annuncio.
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
   * Notifiche che consentono a TVSDK e alla tua applicazione di comunicare in modo asincrono sullo stato di video, annunci pubblicitari e altri elementi , e anche su tale attività di registro

* Registrazione

   * Debug logging
   * Supporto del tracciamento per durata, dimensioni e tempo di download dei frammenti
