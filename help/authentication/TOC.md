---
product: adobe primetime
audience: end-user
feature: Authentication
user-guide-title: Autenticazione Primetime
user-guide-description: Autenticazione Primetime è una soluzione di adesione per TV Everywhere, che fornisce un framework modulare per determinare se qualcuno che richiede l’accesso a una risorsa ne ha diritto.
source-git-commit: 90d6c78791f2fd1bf80979b105d42e019686aacd
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---


# Guida all’autenticazione di Primetime {#authentication}

+ [Panoramica sull’autenticazione Primetime](home.md)
+ Concetti di autenticazione Primetime {#authentication-concepts}
   + [Documento tecnico](technical-paper.md)
   + [Panoramica sui programmatori](programmer-overview.md)
   + [Panoramica di MVPD](mvpd-overview.md)
+ Guide Kick-Start {#kickstart-guides}
   + [Guida introduttiva per programmatori](programmer-kickstart-guide.md)
   + [Guida introduttiva MVPD](mvpd-kickstart-guide.md)
+ Guida all’integrazione dei programmatori {#programmer-integration-guide}
   + [Panoramica della guida all’integrazione dei programmatori](programmer-integration-guide-overview.md)
   + [Flusso adesione programmatore](entitlement-flow.md)
   + [Casi di utilizzo dei programmatori](programmer-use-cases.md)
   + [Trasmissione delle informazioni del client (dispositivo, connessione e applicazione)](passing-client-information-device-connection-and-application.md)
   + API REST {#restapi}
      + [Panoramica API REST](rest-api-overview.md)
      + [Manuale dell’API REST (server-to-server)](rest-api-cookbook-servertoserver.md)
      + [Manuale dell’API REST (da client a server)](rest-api-cookbook-clienttoserver.md)
      + Riferimento API REST {#rest-api-reference}
         + [Riferimento API REST](rest-api-reference.md)
         + [Richiesta codice di registrazione](registration-code-request.md)
         + [Record di registrazione di ritorno](return-registration-record.md)
         + [Elimina record di registrazione](delete-registration-record.md)
         + [Fornisci elenco MVPD](provide-mvpd-list.md)
         + [Avvia autenticazione](initiate-authentication.md)
         + [Controlla token di autenticazione](check-authentication-token.md)
         + [Recupera token di autenticazione](retrieve-authentication-token.md)
         + [Avvia autorizzazione](initiate-authorization.md)
         + [Recupera token di autorizzazione](retrieve-authorization-token.md)
         + [Ottieni token multimediale breve](obtain-short-media-token.md)
         + [Controlla il flusso di autenticazione tramite l’app web Second Screen](check-authentication-flow-by-second-screen-web-app.md)
         + [Recupera elenco risorse autorizzate](retrieve-list-of-preauthorized-resources.md)
         + [Recupera elenco di risorse preautorizzate tramite l’app web Second Screen](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
         + [Avvia disconnessione](initiate-logout.md)
         + [Metadati utente](user-metadata.md)
         + [Recupera richiesta-profilo](retrieve-profilerequest.md)
         + [Scambio di token](token-exchange.md)
         + [Anteprima gratuita per Passaggio temporaneo e Passaggio temporaneo promozionale](free-preview-for-temp-pass-and-promotional-temp-pass.md)
   + SDK di AccessEnabler {#accessenabler-sdk}
      + SDK JavaScript {#javascriptsdk}
         + [Panoramica dell’SDK JavaScript](javascript-sdk-overview.md)
         + [Manuale dell’SDK JavaScript](javascript-sdk-cookbook.md)
         + [Riferimento API dell&#39;SDK JavaScript](javascript-sdk-api-reference.md)
         + Linee guida {#js-sdk-guidelines}
            + [Accesso e disconnessione senza aggiornamento](refreshless-login-and-logout.md)
         + API JavaScript {#js-api}
            + [Autorizza in anticipo](js-preauthorize.md)
      + SDK per iOS/tvOS {#ios-sdk}
         + [Panoramica dell’SDK iOS/tvOS](iostvos-sdk-overview.md)
         + [Manuale dell’SDK iOS/tvOS](iostvos-sdk-cookbook.md)
         + [Riferimento API per iOS/tvOS SDK](iostvos-sdk-api-reference.md)
         + Linee guida {#ios-tvos-sdk-guidelines}
            + [Registrazione applicazione iOS/tvOS](iostvos-application-registration.md)
            + Linee guida per la migrazione {#migration-guidelines}
               + [Guida alla migrazione ad iOS/tvOS v3.x](iostvos-v3x-migration-guide.md)
         + API iOS/tvOS {#ios-tvos-api}
            + [Autorizza in anticipo](preauthorize.md)
      + SDK per Android {#androidsdk}
         + [Panoramica dell’SDK per Android](android-sdk-overview.md)
         + [Manuale dell’SDK per Android](android-sdk-cookbook.md)
         + [Riferimento API dell&#39;SDK per Android](android-sdk-api-reference.md)
         + Linee guida {#androidguidelines}
            + [Registrazione applicazione Android](android-application-registration.md)
            + [SDK per Android con registrazione client dinamica](android-sdk-with-dynamic-client-registration.md)
         + API Android{#androidapi}
            + [Autorizza in anticipo](preauthorize-android.md)
      + SDK di Amazon FireOS {#fireossdk}
         + [Amazon FireOS SSO - Guida introduttiva per il programmatore](amazon-firetv-sso-programmer-kickoff-guide.md)
         + [SSO di Amazon FireOS utilizzando il manuale API senza client](amazon-fireos-sso-using-clientless-api-cookbook.md)
         + [Panoramica tecnica di Amazon FireOS](amazon-fireos-technical-overview.md)
         + [Manuale dell’integrazione di Amazon FireOS](amazon-fireos-integration-cookbook.md)
         + [Riferimento API di Amazon FireOS](amazon-fireos-native-client-api-reference.md)
         + [Registrazione applicazione Amazon FireOS](amazon-fireos-application-registration.md)
         + [SDK FireOS con registrazione client dinamica](fireos-sdk-with-dynamic-client-registration.md)
   + SSO piattaforma {#platform-sso}
      + SSO APPLE {#apple-sso}
         + [Panoramica di Apple SSO](apple-sso-overview.md)
         + [Manuale Apple SSO (REST API)](apple-sso-cookbook-rest-api.md)
         + [Manuale Apple SSO (iOS/tvOS SDK)](apple-sso-cookbook-iostvos-sdk.md)
      + SSO Roku {#roku-sso}
         + [SSO Roku](roku-sso-overview.md)
   + Metadati contenuto {#content-metadata}
      + [Identificazione di una risorsa protetta](identify-protected-resources.md)
   + Integrazione del server dei contenuti {#content-serv-int}
      + [Integrare Media Token Verifier](media-token-verifier-int.md)
   + Appendici {#appendices}
      + [Suggerimenti per il debug](appendix-b-debugging-tips.md)
+ Guida all’integrazione di MVPD {#mvpd-int-guide}
   + [Funzioni di integrazione](mvpd-integr-features.md)
   + [Autenticazione](authn-usecase.md)
   + [Autenticazione tramite il protocollo OAuth 2.0](authn-oauth2-protocol.md)
   + [Autorizzazione](authz-usecase.md)
   + [Autorizzazione di verifica preliminare](mvpd-preflight-authz.md)
   + [Disconnessione MVPD](usecase-mvpd-logout.md)
   + [Scambio di metadati del contenuto](mvpd-content-metadata-exchange.md)
   + [Scambio di metadati utente](mvpd-user-metadata-exchng.md)
   + [Servizio Web MVPD proxy](proxy-mvpd-webserv.md)
   + [Integrazione SAML MVPD proxy](proxy-mvpd-saml-int.md)
   + [Ambito provider di servizi](serv-provider-scoping.md)
   + [Indirizzi IP consentiti MVPD](mvpd-listing-ip-addres.md)
+ Funzioni di autenticazione di Primetime {#auth-features}
   + Integrazione con Adobe Analytics {#analytics-int}
      + [Integrazione dei dati lato server di autenticazione Primetime in Adobe Analytics](integrate-authn-servr-data-analytics.md)
      + [Utilizzo dell’ID Experience Cloud nell’autenticazione Primetime](exp-cloud-id-authn.md)
   + Monitoraggio del servizio di adesione {#entitlement-service-monitoring}
      + [Panoramica sul monitoraggio del servizio di adesione](entitlement-service-monitoring-overview.md)
      + [API di monitoraggio del servizio di adesione](entitlement-service-monitoring-api.md)
      + [Metriche lato server](understanding-serverside-metrics.md)
   + Passaggio temporaneo {#temp-pass}
      + [Passaggio temporaneo](temp-pass.md)
      + [Passaggio temporaneo promozionale](promotional-temp-pass.md)
   + Single Sign-On {#sso}
      + [Supporto del Single Sign-On](sso-support.md)
      + [SSO tramite autenticazione passiva](sso-passive-authn.md)
   + Autenticazione basata su Home {#home-based-auth}
      + [Autenticazione basata su Home per TV Everywhere](home-based-authn-tve.md)
      + [Stato HBA per MVPD](hba-status-mvpds.md)
   + Metadati utente {#user-metadat}
      + [Metadati utente](user-metadata-feature.md)
   + [Autorizzazione di verifica preliminare](preflight-authz.md)
   + Segnalazione di errori {#error-reportn}
      + [Segnalazione di errori](error-reporting.md)
      + [Codici di errore migliorati](enhanced-error-codes.md)
   + Registrazione client {#client-regn}
      + [Registrazione client dinamici](dynamic-client-registration.md)
      + [API di registrazione client dinamica](dynamic-client-registration-api.md)
      + [Dynamic Client Registration Management](dynamic-client-registration-management.md)
   + Servizio di degrado {#degrn-service}
      + [Panoramica dell’API di degradazione](degradation-api-overview.md)
   + Preparazione alla privacy {#privacy-readiness}
      + [Panoramica sul supporto della privacy](privacy-supp-overview.md)
      + [Come effettuare una richiesta di accesso a dati personali](make-privacy-req.md)
+ Suggerimenti e risoluzione dei problemi {#tips-troubleshoot}
   + [Consenti MVPD nella finestra di dialogo di selezione](allow-mvpd-selectn-dialog.md)
   + [Impedisci a MVPDs di visualizzare la finestra di dialogo di selezione](prevent-mvpd-selectn-dialog.md)
+ Supporto {#support}
   + [Procedure di riassegnazione](escalation-procedures.md)
   + [Adobe di monitoraggio Primetime PayTV Pass](monitoring-adobe-pay-tv-pass.md)
   + [Requisiti minimi di sistema](minimum-system-requirements.md)
+ Note sulla versione {#release-notes}
   + [Note sulla versione di Adobe Pass Authentication 2.67](auth-rn-267.md)
   + [Note sulla versione di Adobe Pass Authentication 2.66](auth-rn-266.md)
   + [Note sulla versione di Adobe Pass Authentication 2.65.1](auth-rn-2651.md)
   + [Note sulla versione di Primetime Authentication 2.65](auth-rn-265.md)
   + [Note sulla versione di Primetime Authentication 2.64.1](auth-rn-2641.md)
   + [Note sulla versione di Primetime Authentication 2.64](auth-rn-264.md)
   + [Note sulla versione di Primetime Authentication 2.63](auth-rn-263.md)
   + [Note sulla versione di Primetime Authentication 2.62.1](auth-rn-2621.md)
   + [Note sulla versione di iOS/tvOS 3.7.0 per l’autenticazione Primetime](authn-rn-ios-tvos-370.md)
   + [Note sulla versione di Primetime Authentication iOS/tvOS 3.8.1](authn-rn-ios-tvos-381.md)
+ Note tecniche {#tech-notes}
   + SDK per autenticazione Primetime {#primetime-authentication-sdks}
      + [Domande e risposte sui certificati](certificates-qa.md)
      + SDK JavaScript {#javascript}
         + [Limitazioni dell’SDK JS per il browser Safari](js-sdk-limitations-for-safari-browser.md)
         + [Aggiornamenti dei cookie - Flag SameSite e Secure](cookies-updates--samesite-and-secure-flags.md)
      + SDK per Android {#android}
         + [Accesso a Single Sign-On (SSO) SDK per Android su app Android 10](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
         + [Autenticazione Adobe Primetime e il nuovo modello di autorizzazioni &quot;Marshmallow&quot; per Android 6](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
      + SDK per iOS/tvOS {#iostvos}
         + [Supporto WKWebView sull&#39;SDK iOS 3.1+](wkwebview-support-on-ios-sdk-31.md)
         + [Supporto di SFSafariViewController sull&#39;SDK iOS 3.2+](sfsafariviewcontroller-support-on-ios-sdk-32.md)
         + [SSO su iOS quando si utilizza l’attivatore di accesso per l’autenticazione Primetime](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
         + [Errore di autenticazione iOS - Impossibile trovare adobepass.ios.app](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
         + [Ripristina passaggio temporaneo su iOS](reset-temp-pass-on-ios.md)
         + [Debug dell’SDK iOS/tvOS di AccessEnabler tramite i registri dell’app della console](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
         + [Percorso di aggiornamento ad AccessEnabler iOS/tvOS 3.7.0](accessenabler-iostvos-370-upgrade-path.md)
   + Ambienti di autenticazione Primetime {#primetime-authentication-environments}
      + [Informazioni sugli ambienti Adobe](understanding-the-adobe-environments.md)
      + [Configurazione dell’ambiente e test in Pre-Qual](setting-up-your-environment-and-testing-in-prequal.md)
      + [Verificare i flussi di autenticazione e autorizzazione utilizzando il sito di test API Adobe](test-authn-authz-flows-using-adobes-api-test-site.md)
   + API senza client {#clientless-api}
      + [Implementazione API senza client - Codici di errore/messaggi con motivo/causa probabile](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
      + [Flusso API senza client in assenza di ID dispositivo](clientless-api-flow-in-the-absence-of-device-id.md)
      + [Clientless: evita di utilizzare &#39;&amp;&#39;reg_code nella richiesta /authenticate](clientless-avoid-using-reg-code-in-authenticate-request.md)
      + [Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e Xbox One Clientless](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
      + [Tipo di dispositivo e metriche senza client](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
   + Esperienza utente {#user-exp}
      + [Come migrare la pagina di accesso MVPD da iFrame a popup](migr-mvpd-login-iframe-popup.md)
      + [Funzione di verifica preliminare: come abilitare, risolvere o determinare il problema](preflight-feature.md)
   + Strumenti e utilità {#tools-and-utilities}
      + [Utilizzo di Charles Proxy](using-charles-proxy.md)
   + Concetti {#concepts}
      + [Informazioni sugli ID utente](understanding-user-ids.md)
+ [Guida utente di TVE Dashboard](tve-dashboard-user-guide.md)
+ [Glossario](glossary.md)
