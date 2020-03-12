---
description: 'TVSDK per desktop HLS include una varietà di funzionalità e fornisce le seguenti funzionalità principali '
seo-description: 'TVSDK per desktop HLS include una varietà di funzionalità e fornisce le seguenti funzionalità principali '
seo-title: Funzioni Primetime TVSDK
title: Funzioni Primetime TVSDK
uuid: 0a7ebb05-7da5-49ff-928a-4d2124eaa115
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# Funzioni Primetime TVSDK{#primetime-tvsdk-features}

TVSDK per desktop HLS include una serie di funzionalità e offre le seguenti funzionalità principali:

* VOD e riproduzione live/lineare

   * Gestione della finestra di riproduzione, compresi i metodi che consentono di riprodurre, interrompere, mettere in pausa, cercare e recuperare la posizione dell&#39;indicatore di riproduzione.
   * Sottotitoli codificati (608, 708, WebVTT) e moduli audio alternativi per una maggiore accessibilità
   * Controllo dello stile del testo nelle didascalie
   * Funzionalità DVR, riavvolgimento rapido/rapido (modalità &quot;play&quot;)
   * Riproduzione di mattoni per contenuti live e VOD
   * Logica di bitrate adattivo (ABR) e configurazione iniziale dei controlli ABR
   * Supporto del failover del manifesto in diretta
   * Buffer di riproduzione regolabili
   * Ottimizzazione reindirizzamento 302
   * Supporto per il tracciamento della durata, delle dimensioni e del tempo di scaricamento dei frammenti

* Pubblicità

   * VPAID 2.0
   * Cuciture lato client

      * Inserimento di annunci senza problemi, compreso il supporto per VAST/VMAP
      * Supporto per i tag cue personalizzati per gli annunci
      * Supporto per la marcatura, la sostituzione e l&#39;eliminazione di annunci C3
      * Flusso di lavoro personalizzabile per l’inserimento di contenuti/annunci, compresa la segnalazione di blackout

* Protezione dei contenuti

   * Accesso ai servizi relativi alla gestione dei diritti digitali (DRM)
   * Riproduzione di flussi HLS non crittografati o con lo streaming HTTP Live protetto (PHLS)
   * Controllo dell&#39;output basato sulla risoluzione, basato su criteri DRM
   * Supporto di cookie di sessione e cookie di autenticazione multimediale
   * Pacchetto di token a più domini

* Tracciamento di video e annunci

   * Tracciamento evento QoS
   * Notifiche che aiutano TVSDK e la tua applicazione a comunicare in modo asincrono lo stato di video, annunci pubblicitari e altri elementi, nonché l&#39;attività di registro.
   * Integrazione con Adobe Analytics e supporto heartbeat

* Registrazione

   * Debug della registrazione.
   * Supporto per il monitoraggio di durata, dimensioni e tempo di download dei frammenti.