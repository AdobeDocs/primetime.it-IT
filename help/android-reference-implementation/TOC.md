---
cloud: experience-cloud
product: primetime
audience: end-user
user-guide-title: Guida all’implementazione di riferimento Primetime
user-guide-description: Helps understand the TVSDK and modify the feature managers to customize your personal player.
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# PSDK 1.4 per l&#39;implementazione di riferimento Android {#reference-implementation}

+ [Panoramica dell&#39;implementazione di riferimento per Android](home.md)
+ Implementazione di riferimento Primetime {#reference}
   + [Come utilizzare l&#39;implementazione di riferimento Primetime](ref-implementation/how-to-use-ref-player.md)
   + [Struttura di implementazione di riferimento](ref-implementation/ref-player-structure.md)
   + Come utilizzare i feature manager {#feature-managers}
      + [Come utilizzare i feature manager](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Creazione di feature manager trasmettendo le informazioni di configurazione a MediaPlayer...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Attivazione o disattivazione delle funzioni tramite ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Gestione degli eventi](ref-implementation/using-feature-managers/handling-events.md)
   + Configurare l&#39;ambiente di sviluppo {#setup-dev}
      + [Configurare l&#39;ambiente di sviluppo](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Download e configurazione del software prerequisito](set-up-dev-environment/download-prereqs-android.md)
      + [Creare l&#39;implementazione di riferimento Primetime](set-up-dev-environment/install-the-ref-player-project.md)
   + Esplora il codice {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Feature manager](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Formato catalogo](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Oggetto JSON per annunci Primetime](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [Oggetto JSON per interruzioni pubblicitarie dirette](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [Oggetto JSON per marcatori di annunci personalizzati](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [Oggetto JSON per ID risorsa di adesione](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Esempio di formato di feed JSON](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implementare la riproduzione video {#implement-video}
      + [Operazioni essenziali di riproduzione video](implement-video-playback/video-playback.md)
      + [Abilita riproduzione video](implement-video-playback/enable-video-playback.md)
      + [Protezione dei contenuti DRM](implement-video-playback/content-protection.md)
   + [Bitrate multipli](implement-video-playback/mbr.md)
   + Impostare un lettore per la riproduzione DVR con gli annunci {#dvr}
      + [DVR senza inserimento annunci](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [DVR con inserimento annunci](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [Scelta di un punto di partenza personalizzato per il DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [Impostazione di un&#39;ora di inizio personalizzata nell&#39;implementazione di riferimento](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Visualizzare le statistiche sulla riproduzione e sul dispositivo QoS](implement-video-playback/qos-statistics.md)
   + Inserire annunci {#insert-ads}
      + [Inserimento annunci](insert-ads/ad-insertion.md)
      + [Tipi di inserimento annunci](insert-ads/ad-insertion-types.md)
      + [Aggiunta di pubblicità](insert-ads/add-advertising.md)
      + [Documentazione API correlata](insert-ads/aps-callbacks-ad-insertion.md)
   + Connessione audio ritardata {#late-binding-audio}
      + [Panoramica](late-binding-audio/late-binding-audio-overview.md)
      + [Integrare l&#39;audio con binding ritardato](late-binding-audio/aa-enable.md)
      + [Selezionare le tracce audio](late-binding-audio/select-audio-tracks.md)
      + [Documentazione API correlata](late-binding-audio/aa-api-callbacks.md)
   + Flussi di adesione per l&#39;autenticazione Primetime {#primetime-authentications}
      + [Panoramica](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [Panoramica di Entitlement Manager](paytvpass-entitlement/entitlement-overvivew.md)
      + [Integrare l&#39;autenticazione Primetime](paytvpass-entitlement/integrate-pass.md)
      + [Configurare  rapporti Adobe Analytics](paytvpass-entitlement/pass-analytics-setup.md)
      + [Documentazione API correlata](paytvpass-entitlement/pass-apis-callbacks.md)
   + Analisi video {#video-analytics}
      + [Analisi video](video-analytics/video-analytics-overview.md)
      + [Creare Video Analytics Manager](video-analytics/create-video-analytics-manager.md)
      + [Configurare l&#39;analisi video](video-analytics/configure-video-analytics-manager.md)
      + [Documentazione API correlata](video-analytics/va-apis-callbacks.md)
   + [Creare un&#39;interfaccia utente personalizzata](build-custom-ui.md)
   + [Risoluzione dei problemi](troubleshooting.md)
