---
description: TVSDK per Android 3.4 include una varietà di funzioni che puoi implementare nei lettori.
title: Funzioni di Primetime TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Funzioni di Primetime TVSDK {#primetime-tvsdk-features}

TVSDK per Android 3.9 include una varietà di funzioni che puoi implementare nei lettori.

Funzionalità TVSDK:

* **VOD e riproduzione live/lineare**

   * Gestione della finestra di riproduzione, inclusi i metodi di riproduzione, arresto, pausa, ricerca e recupero della posizione della testina di riproduzione
   * Supporto per la riproduzione completa degli eventi
   * Sottotitoli codificati (608, 708, WebVTT) e forme alternative di audio per una maggiore accessibilità
   * Controlli per lo stile del testo nei sottotitoli
   * Capacità DVR, avanzamento rapido e riavvolgimento rapido (gli ultimi due sono noti come *modalità trick-play*)
   * Logica di bit rate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Supporto del failover del manifesto live
   * Buffer di riproduzione regolabili
   * Supporto del tracciamento per durata, dimensione e tempo di download dei frammenti

* **Pubblicità**

   * VPAID 2.0
   * Unione di annunci lato client

      * Inserimento semplice degli annunci, incluso il supporto per VAST/VMAP
      * Supporto di tag di cue personalizzati per gli annunci
      * Supporto per contrassegnare, sostituire ed eliminare annunci C3
      * Flusso di lavoro personalizzabile per l&#39;inserimento di contenuti/annunci, inclusa la segnalazione di sospensione attività

* **Protezione dei contenuti**

   * Accesso ai servizi correlati alla gestione dei diritti digitali (DRM)
   * Riproduzione di flussi HLS non crittografati o con Protected HTTP Live Streaming (PHLS)
   * Controllo dell&#39;output basato su risoluzione, basato su regole DRM

* **Tracciamento di video e annunci**

   * Tracciamento eventi QoS
   * Notifiche che consentono a TVSDK e all’applicazione di comunicare in modo asincrono sullo stato di video, annunci pubblicitari e altri elementi. Le notifiche registrano anche l’attività.

* **Registrazione**

   * Debug logging
   * Supporto del tracciamento per durata, dimensioni e tempo di download dei frammenti.

* **Consegna sicura**

   * Supporto di Secure Delivery (HTTPS) per tutte le chiamate provenienti da TVSDK.
