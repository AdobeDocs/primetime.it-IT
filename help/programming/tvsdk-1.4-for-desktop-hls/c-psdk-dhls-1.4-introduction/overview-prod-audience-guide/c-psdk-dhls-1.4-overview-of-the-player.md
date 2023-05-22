---
description: TVSDK per HLS desktop include una serie di funzioni e fornisce le seguenti funzionalità principali
title: Funzioni di Primetime TVSDK
exl-id: d78ca77e-b29c-4fae-8ab9-edc55ab12847
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Funzioni di Primetime TVSDK{#primetime-tvsdk-features}

TVSDK per HLS desktop include una serie di funzioni e fornisce le seguenti funzionalità principali:

* VOD e riproduzione live/lineare

   * Gestione della finestra di riproduzione, inclusi i metodi di riproduzione, arresto, pausa, ricerca e recupero della posizione della testina di riproduzione.
   * Sottotitoli codificati (608, 708, WebVTT) e forme alternative di audio per una maggiore accessibilità
   * Controllo per lo stile del testo nei sottotitoli
   * Capacità DVR, avanzamento rapido/riavvolgimento rapido (modalità di riproduzione con selezione)
   * Riproduzione dei brani sia per contenuti live che VOD
   * Logica di bit rate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Supporto del failover del manifesto live
   * Buffer di riproduzione regolabili
   * Ottimizzazione del reindirizzamento 302
   * Supporto del tracciamento per durata, dimensione e tempo di download dei frammenti

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
   * Supporto cookie di sessione e cookie di autenticazione dei contenuti multimediali
   * Pacchetto di token per più domini

* Tracciamento di video e annunci

   * Tracciamento eventi QoS
   * Notifiche che consentono a TVSDK e all’applicazione di comunicare in modo asincrono sullo stato di video, annunci pubblicitari e altri elementi, nonché su tale attività di registro.
   * Integrazione con Adobe Analytics e supporto heartbeat

* Registrazione

   * Registrazione debug.
   * Supporto del tracciamento per durata, dimensioni e tempo di download dei frammenti.
