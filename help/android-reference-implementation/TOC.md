---
product: primetime
audience: end-user
user-guide-title: Guida all’implementazione di Primetime
user-guide-description: Consente di comprendere il TVSDK e modificare i gestori delle funzioni per personalizzare il lettore personale.
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# PSDK 1.4 per implementazione di riferimento Android {#reference-implementation}

+ [Panoramica dell’implementazione di riferimento Android](home.md)
+ Implementazione di riferimento di Primetime {#reference}
   + [Come utilizzare l’implementazione di riferimento di Primetime](ref-implementation/how-to-use-ref-player.md)
   + [Struttura di implementazione di riferimento](ref-implementation/ref-player-structure.md)
   + Come utilizzare i gestori di funzionalità {#feature-managers}
      + [Come utilizzare i gestori di funzionalità](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Creazione di gestori di funzionalità mediante la trasmissione delle informazioni di configurazione a MediaPlayer in corso...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Attivazione o disattivazione delle feature mediante ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Gestione degli eventi](ref-implementation/using-feature-managers/handling-events.md)
   + Configurare l’ambiente di sviluppo {#setup-dev}
      + [Configurare l’ambiente di sviluppo](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Scaricare e configurare i prerequisiti software](set-up-dev-environment/download-prereqs-android.md)
      + [Creare l’implementazione di riferimento di Primetime](set-up-dev-environment/install-the-ref-player-project.md)
   + Esplora il codice {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Feature manager](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Formato catalogo](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Oggetto JSON per annunci Primetime](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [Oggetto JSON per interruzioni pubblicitarie dirette](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [Oggetto JSON per marcatori di annunci personalizzati](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [Oggetto JSON per ID risorsa adesione](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Esempio di formato del feed JSON](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implementare la riproduzione video {#implement-video}
      + [Operazioni essenziali di riproduzione video](implement-video-playback/video-playback.md)
      + [Abilita riproduzione video](implement-video-playback/enable-video-playback.md)
      + [Protezione dei contenuti DRM](implement-video-playback/content-protection.md)
   + [Velocità bit multiple](implement-video-playback/mbr.md)
   + Configurare un lettore per la riproduzione DVR con annunci {#dvr}
      + [DVR senza inserimento di annunci](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [DVR con inserimento di annunci](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [Scelta di un punto di partenza personalizzato per il DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [Impostare un’ora di inizio personalizzata nell’implementazione di riferimento](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Visualizzare le statistiche della riproduzione QoS e del dispositivo](implement-video-playback/qos-statistics.md)
   + Inserisci annunci {#insert-ads}
      + [Inserimento di annunci](insert-ads/ad-insertion.md)
      + [Tipi di inserimento di annunci](insert-ads/ad-insertion-types.md)
      + [Aggiungi pubblicità](insert-ads/add-advertising.md)
      + [Documentazione API correlata](insert-ads/aps-callbacks-ad-insertion.md)
   + Audio di associazione tardiva {#late-binding-audio}
      + [Panoramica](late-binding-audio/late-binding-audio-overview.md)
      + [Integrare l’audio di associazione tardiva](late-binding-audio/aa-enable.md)
      + [Selezionare le tracce audio](late-binding-audio/select-audio-tracks.md)
      + [Documentazione API correlata](late-binding-audio/aa-api-callbacks.md)
   + Flussi di adesione all’autenticazione Primetime {#primetime-authentications}
      + [Panoramica](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [Panoramica di Gestione diritti](paytvpass-entitlement/entitlement-overvivew.md)
      + [Integrare l’autenticazione Primetime](paytvpass-entitlement/integrate-pass.md)
      + [Configurare il reporting di Adobe Analytics](paytvpass-entitlement/pass-analytics-setup.md)
      + [Documentazione API correlata](paytvpass-entitlement/pass-apis-callbacks.md)
   + Analisi dei video {#video-analytics}
      + [Analisi dei video](video-analytics/video-analytics-overview.md)
      + [Creare Video Analytics Manager](video-analytics/create-video-analytics-manager.md)
      + [Configurazione analisi video](video-analytics/configure-video-analytics-manager.md)
      + [Documentazione API correlata](video-analytics/va-apis-callbacks.md)
   + [Creare un’interfaccia utente personalizzata](build-custom-ui.md)
   + [Risoluzione dei problemi](troubleshooting.md)
