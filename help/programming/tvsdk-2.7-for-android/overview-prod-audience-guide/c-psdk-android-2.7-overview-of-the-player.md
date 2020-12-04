---
description: TVSDK per Android 2.5 include una serie di funzionalità che puoi implementare nei lettori.
seo-description: TVSDK per Android 2.5 include una serie di funzionalità che puoi implementare nei lettori.
seo-title: Funzioni Primetime TVSDK
title: Funzioni Primetime TVSDK
uuid: 20ef9abf-1a33-4afc-bb2e-4910e3398a7a
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Funzioni Primetime TVSDK {#primetime-tvsdk-features}

TVSDK per Android 2.7 include una serie di funzionalità che puoi implementare nei lettori.

Funzionalità TVSDK:

* **VOD e riproduzione live/lineare**

   * Gestione della finestra di riproduzione, compresi i metodi che riproducono, fermano, mettono in pausa, cercano e recuperano la posizione della testina di riproduzione
   * Supporto per la riproduzione a tutti gli eventi
   * Sottotitoli codificati (608, 708, WebVTT) e moduli audio alternativi per una maggiore accessibilità
   * Controlli per lo stile del testo nelle didascalie
   * Funzionalità DVR, avanzamento rapido e riavvolgimento rapido (gli ultimi due sono noti come *modalità &quot;trucco-play&quot;*)
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