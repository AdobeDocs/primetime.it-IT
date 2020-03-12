---
description: TVSDK per Android 3.4 include una serie di funzionalità che puoi implementare nei lettori.
seo-description: TVSDK per Android 3.4 include una serie di funzionalità che puoi implementare nei lettori.
seo-title: Funzioni Primetime TVSDK
title: Funzioni Primetime TVSDK
uuid: 6e26c09c-2858-47d1-80e8-1d7c6a468b86
translation-type: tm+mt
source-git-commit: ad58732842eb651514a47dd565e31e3d98a84c46

---


# Funzioni Primetime TVSDK {#primetime-tvsdk-features}

TVSDK per Android 3.9 include una serie di funzionalità che puoi implementare nei lettori.

Funzionalità TVSDK:

* **VOD e riproduzione live/lineare**

   * Gestione della finestra di riproduzione, compresi i metodi che riproducono, fermano, mettono in pausa, cercano e recuperano la posizione della testina di riproduzione
   * Supporto per la riproduzione a tutti gli eventi
   * Sottotitoli codificati (608, 708, WebVTT) e moduli audio alternativi per una maggiore accessibilità
   * Controlli per lo stile del testo nelle didascalie
   * Funzionalità DVR, avanzamento rapido e riavvolgimento rapido (le ultime due sono note come modalità ** trucco)
   * Logica di bitrate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Supporto del failover del manifesto in diretta
   * Buffer di riproduzione regolabili
   * Supporto per il tracciamento della durata, delle dimensioni e del tempo di scaricamento dei frammenti

* **Pubblicità**

   * VPAID 2.0
   * Cuciture lato client

      * Inserimento di annunci senza problemi, compreso il supporto per VAST/VMAP
      * Supporto per i tag cue personalizzati per gli annunci
      * Supporto per la marcatura, la sostituzione e l&#39;eliminazione di annunci C3
      * Flusso di lavoro personalizzabile per l’inserimento di contenuti/annunci, compresa la segnalazione di blackout

* **Protezione dei contenuti**

   * Accesso ai servizi relativi alla gestione dei diritti digitali (DRM)
   * Riproduzione di flussi HLS non crittografati o con lo streaming HTTP Live protetto (PHLS)
   * Controllo dell&#39;output basato sulla risoluzione, basato su criteri DRM

* **Tracciamento di video e annunci**

   * Tracciamento evento QoS
   * Notifiche che aiutano TVSDK e la tua applicazione a comunicare in modo asincrono lo stato di video, annunci pubblicitari e altri elementi. Notifiche anche attività di registro.

* **Registrazione**

   * Debug logging
   * Supporto per il monitoraggio di durata, dimensioni e tempo di download dei frammenti.

* **Consegna sicura**

   * Supporto per la consegna protetta (HTTPS) per tutte le chiamate provenienti da TVSDK.