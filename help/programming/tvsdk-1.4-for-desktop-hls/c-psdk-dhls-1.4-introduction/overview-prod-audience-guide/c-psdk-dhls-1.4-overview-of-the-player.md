---
description: 'TVSDK per HLS desktop include una varietà di funzioni e fornisce le seguenti funzionalità principali '
title: Funzioni TVSDK di Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Funzioni TVSDK di Primetime{#primetime-tvsdk-features}

TVSDK per Desktop HLS include una serie di funzioni e fornisce le seguenti funzionalità principali:

* Riproduzione VOD e live/lineare

   * Gestione della finestra di riproduzione, compresi i metodi che riproducono, fermano, mettono in pausa, cercano e recuperano la posizione della testina di riproduzione.
   * Sottotitoli codificati (608, 708, WebVTT) e moduli audio alternativi per una maggiore accessibilità
   * Controllo dello stile del testo nelle didascalie
   * Funzione DVR, avanzamento rapido/riavvolgimento rapido (modalità &quot;play&quot;)
   * Riproduzione a mattoni per contenuti live e VOD
   * Logica del bit rate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Supporto del failover del manifesto in tempo reale
   * Buffer di riproduzione regolabili
   * Ottimizzazione del reindirizzamento 302
   * Supporto per il tracciamento di tempi e dimensioni dei frammenti e del tempo necessario per il download

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
   * Supporto per cookie di sessione e cookie di autenticazione dei contenuti multimediali
   * Pacchetto di token a più domini

* Tracciamento video e annunci

   * Tracciamento degli eventi QoS
   * Notifiche che aiutano TVSDK e la tua applicazione a comunicare in modo asincrono lo stato dei video, degli annunci pubblicitari e di altri elementi, nonché l’attività di log.
   * Integrazione con Adobe Analytics e supporto heartbeat

* Registrazione

   * Debug della registrazione.
   * Supporto per il tracciamento di durata, dimensioni e tempo di download dei frammenti.