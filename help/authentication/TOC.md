---
product: adobe primetime
audience: end-user
user-guide-title: Autenticazione Primetime
user-guide-description: Primetime Authentication è una soluzione di adesione per TV Everywhere, che fornisce un framework modulare per determinare se qualcuno che richiede l'accesso a una risorsa ne ha diritto.
source-git-commit: 9ce554b32564727488f85cef62abd5ce9c1c21f1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Guida all’autenticazione di Primetime {#authentication}

+ [Panoramica sull’autenticazione di Primetime](home.md)
+ Concetti di autenticazione di Primetime {#authentication-concepts}
   + [Carta tecnica](technical-paper.md)
   + [Panoramica per programmatori](programmer-overview.md)
   + [Panoramica MVPD](mvpd-overview.md)
+ Guide al kickstart {#kickstart-guides}
   + [Guida rapida per programmatori](programmer-kickstart-guide.md)
   + [Guida rapida MVPD](mvpd-kickstart-guide.md)
+ Guida all’integrazione dei programmatori {#programmer-integration-guide}
   + [Panoramica sull’integrazione dei programmatori](programmer-integration-guide-overview.md)
   + [Flusso di adesione del programmatore](entitlement-flow.md)
   + [Casi d&#39;uso del programmatore](programmer-use-cases.md)
   + [Trasferimento delle informazioni sul client (dispositivo, connessione e applicazione)](passing-client-information-device-connection-and-application.md)
   + API REST {#restapi}
      + [Panoramica API REST](rest-api-overview.md)
      + [Guida di riferimento API REST (server-to-server)](rest-api-cookbook-servertoserver.md)
      + [Guida di riferimento API REST (da client a server)](rest-api-cookbook-clienttoserver.md)
      + Riferimento API per il resto {#rest-api-reference}
         + [Riferimento API REST](rest-api-reference.md)
         + [Richiesta codice di registrazione](registration-code-request.md)
         + [Record di registrazione del ritorno](return-registration-record.md)
         + [Elimina record di registrazione](delete-registration-record.md)
         + [Fornire l&#39;elenco MVPD](provide-mvpd-list.md)
         + [Avvia autenticazione](initiate-authentication.md)
         + [Verifica token di autenticazione](check-authentication-token.md)
         + [Recupera token di autenticazione](retrieve-authentication-token.md)
         + [Avvia autorizzazione](initiate-authorization.md)
         + [Recupera token di autorizzazione](retrieve-authorization-token.md)
         + [Ottieni token multimediale breve](obtain-short-media-token.md)
         + [Controlla il flusso di autenticazione in base all&#39;app Web a seconda schermata](check-authentication-flow-by-second-screen-web-app.md)
         + [Recupera elenco risorse preautorizzate](retrieve-list-of-preauthorized-resources.md)
         + [Recupera l&#39;elenco delle risorse preautorizzate dalla seconda schermata Web App](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
         + [Avvia disconnessione](initiate-logout.md)
         + [Metadati utente](user-metadata.md)
         + [Recupera richiesta profilo](retrieve-profilerequest.md)
         + [Token Exchange](token-exchange.md)
         + [Anteprima gratuita per Temp Pass e Promozionale Temp Pass](free-preview-for-temp-pass-and-promotional-temp-pass.md)
   + SDK di AccessEnabler {#accessenabler-sdk}
      + SDK JavaScript {#javascriptsdk}
         + [Panoramica dell&#39;SDK JavaScript](javascript-sdk-overview.md)
         + [Guida di riferimento rapida per l’SDK JavaScript](javascript-sdk-cookbook.md)
         + [Riferimento API SDK JavaScript](javascript-sdk-api-reference.md)
         + Linee guida {#js-sdk-guidelines}
            + [Accesso e disconnessione senza aggiornamento](refreshless-login-and-logout.md)
         + API JavaScript {#js-api}
            + [Autorizzare](js-preauthorize.md)
      + SDK iOS/tvOS {#ios-sdk}
         + [Panoramica dell&#39;SDK per iOS/tvOS](iostvos-sdk-overview.md)
         + [Guida di riferimento rapido per l&#39;SDK di iOS/tvOS](iostvos-sdk-cookbook.md)
         + [Guida di riferimento dell&#39;API SDK per iOS/tvOS](iostvos-sdk-api-reference.md)
         + Linee guida {#ios-tvos-sdk-guidelines}
            + [Registrazione dell&#39;applicazione iOS/tvOS](iostvos-application-registration.md)
            + Linee guida sulla migrazione {#migration-guidelines}
               + [Guida alla migrazione a iOS/tvOS v3.x](iostvos-v3x-migration-guide.md)
         + API iOS/tvOS {#ios-tvos-api}
            + [Autorizzare](preauthorize.md)
      + SDK per Android {#androidsdk}
         + [Panoramica dell’SDK per Android](android-sdk-overview.md)
         + [Guida di riferimento dettagliata per l&#39;SDK Android](android-sdk-cookbook.md)
         + [Riferimento API per l’SDK per Android](android-sdk-api-reference.md)
         + Linee guida {#androidguidelines}
            + [Registrazione dell&#39;applicazione Android](android-application-registration.md)
            + [SDK per Android con registrazione client dinamica](android-sdk-with-dynamic-client-registration.md)
         + API Android{#androidapi}
            + [Autorizzare](preauthorize-android.md)
      + Amazon FireOS SDK {#fireossdk}
         + [Amazon FireOS SSO - Guida introduttiva al programmatore](amazon-firetv-sso-programmer-kickoff-guide.md)
         + [Amazon FireOS SSO tramite il cookie API Clientless](amazon-fireos-sso-using-clientless-api-cookbook.md)
         + [Panoramica tecnica di Amazon FireOS](amazon-fireos-technical-overview.md)
         + [Guida di riferimento per l’integrazione di Amazon FireOS](amazon-fireos-integration-cookbook.md)
         + [Riferimento API di Amazon FireOS](amazon-fireos-native-client-api-reference.md)
         + [Registrazione dell&#39;applicazione Amazon FireOS](amazon-fireos-application-registration.md)
         + [SDK FireOS con registrazione client dinamica](fireos-sdk-with-dynamic-client-registration.md)
   + Piattaforma SSO {#platform-sso}
      + Apple SSO {#apple-sso}
         + [Panoramica di Apple SSO](apple-sso-overview.md)
         + [Cookie Apple SSO (REST API)](apple-sso-cookbook-rest-api.md)
         + [Cookie Apple SSO (iOS/tvOS SDK)](apple-sso-cookbook-iostvos-sdk.md)
      + Roku SSO {#roku-sso}
         + [Roku SSO](roku-sso-overview.md)
   + Metadati del contenuto {#content-metadata}
      + [Identificazione della risorsa protetta](identify-protected-resources.md)
   + Integrazione del server dei contenuti {#content-serv-int}
      + [Come integrare Media Token Verifier](media-token-verifier-int.md)
   + Appendici {#appendices}
      + [Suggerimenti per il debug](appendix-b-debugging-tips.md)
+ Guida all&#39;integrazione MVPD {#mvpd-int-guide}
   + [Funzionalità di integrazione](mvpd-integr-features.md)
   + [Autenticazione](authn-usecase.md)
   + [Autenticazione tramite il protocollo OAuth 2.0](authn-oauth2-protocol.md)
   + [Autorizzazione](authz-usecase.md)
   + [Autorizzazione del volo preliminare](mvpd-preflight-authz.md)
   + [Logout MVPD](usecase-mvpd-logout.md)
   + [Scambio di metadati dei contenuti](mvpd-content-metadata-exchange.md)
   + [Scambio di metadati utente](mvpd-user-metadata-exchng.md)
   + [Servizio Web MVPD proxy](proxy-mvpd-webserv.md)
   + [Integrazione SAML MVPD proxy](proxy-mvpd-saml-int.md)
   + [Ambito del provider di servizi](serv-provider-scoping.md)
   + [Indirizzi IP consentiti MVPD](mvpd-listing-ip-addres.md)
+ Funzioni di autenticazione di Primetime {#auth-features}
   + Integrazione Adobe Analytics {#analytics-int}
      + [Integrazione dei dati lato server di autenticazione Primetime in Adobe Analytics](integrate-authn-servr-data-analytics.md)
      + [Utilizzo dell&#39;ID di Experience Cloud nell&#39;autenticazione di Primetime](exp-cloud-id-authn.md)
   + Monitoraggio dei servizi di autorizzazione {#entitlement-service-monitoring}
      + [Panoramica sul monitoraggio del servizio di autorizzazione](entitlement-service-monitoring-overview.md)
      + [API di monitoraggio del servizio di adesione](entitlement-service-monitoring-api.md)
      + [Metriche lato server](understanding-serverside-metrics.md)
   + Passaggio temporaneo {#temp-pass}
      + [Passaggio temporaneo](temp-pass.md)
      + [Passaggio temporaneo promozionale](promotional-temp-pass.md)
   + Single Sign-On {#sso}
      + [Supporto single sign-on](sso-support.md)
      + [SSO tramite autenticazione passiva](sso-passive-authn.md)
   + Autenticazione basata su home {#home-based-auth}
      + [Autenticazione basata su casa per TV Everywhere](home-based-authn-tve.md)
      + [Stato dell&#39;HBA per gli MVPD](hba-status-mvpds.md)
   + Metadati utente {#user-metadat}
      + [Metadati utente](user-metadata-feature.md)
   + [Autorizzazione del volo preliminare](preflight-authz.md)
   + Segnalazione errori {#error-reportn}
      + [Segnalazione errori](error-reporting.md)
      + [Codici di errore migliorati](enhanced-error-codes.md)
   + Registrazione client {#client-regn}
      + [Registrazione client dinamica](dynamic-client-registration.md)
      + [API di registrazione client dinamica](dynamic-client-registration-api.md)
      + [Dynamic Client Registration Management](dynamic-client-registration-management.md)
   + Servizio di degradazione {#degrn-service}
      + [Panoramica dell’API di degradazione](degradation-api-overview.md)
   + Preparazione alla privacy {#privacy-readiness}
      + [Panoramica sul supporto per la privacy](privacy-supp-overview.md)
      + [Come effettuare una richiesta di accesso a dati personali](make-privacy-req.md)
+ Suggerimenti e risoluzione dei problemi {#tips-troubleshoot}
   + [Consenti MVPD nella finestra di dialogo di selezione](allow-mvpd-selectn-dialog.md)
   + [Impedisci agli MVPD di visualizzare la finestra di dialogo di selezione](prevent-mvpd-selectn-dialog.md)
+ Supporto {#support}
   + [Procedure per l&#39;escalation](escalation-procedures.md)
   + [Monitoraggio del pass PayTV Adobe Primetime](monitoring-adobe-pay-tv-pass.md)
   + [Requisiti minimi di sistema](minimum-system-requirements.md)
+ Note sulla versione {#release-notes}
   + [Note sulla versione di Primetime Authentication 2.64.1](auth-rn-2641.md)
   + [Note sulla versione di Primetime Authentication 2.64](auth-rn-264.md)
   + [Note sulla versione di Primetime Authentication 2.63](auth-rn-263.md)
   + [Note sulla versione di Primetime Authentication iOS / tvOS 3.7.0](authn-rn-ios-tvos-370.md)
+ Note tecniche {#tech-notes}
   + SDK per autenticazione di Primetime {#primetime-authentication-sdks}
      + [Domande e risposte sui certificati](certificates-qa.md)
      + SDK JavaScript {#javascript}
         + [Limitazioni dell’SDK JS per il browser Safari](js-sdk-limitations-for-safari-browser.md)
         + [Aggiornamenti dei cookie - Flag SameSite e Secure](cookies-updates--samesite-and-secure-flags.md)
      + SDK per Android {#android}
         + [Accesso a Single Sign-On (SSO) per Android SDK Enabler su Android 10 app](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
         + [Autenticazione Adobe Primetime e il nuovo modello di autorizzazioni &quot;Marshmallow&quot; per Android 6](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
      + SDK iOS/tvOS {#iostvos}
         + [Supporto WKWebView su iOS SDK 3.1+](wkwebview-support-on-ios-sdk-31.md)
         + [Supporto SFSafariViewController in iOS SDK 3.2+](sfsafariviewcontroller-support-on-ios-sdk-32.md)
         + [SSO su iOS quando si utilizza Primetime Authentication Access Enabler](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
         + [Errore Di Autenticazione iOS - Impossibile Trovare adobepass.ios.app](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
         + [Ripristino di Temp Pass su iOS](reset-temp-pass-on-ios.md)
         + [Debug dell’SDK iOS/tvOS di AccessEnabler tramite i registri delle app della console](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
         + [Percorso di aggiornamento di AccessEnabler iOS/tvOS 3.7.0](accessenabler-iostvos-370-upgrade-path.md)
   + Ambienti di autenticazione di Primetime {#primetime-authentication-environments}
      + [Informazioni sugli ambienti Adobe](understanding-the-adobe-environments.md)
      + [Impostazione dell&#39;ambiente e test in Pre-Qual](setting-up-your-environment-and-testing-in-prequal.md)
      + [Come testare i flussi di autenticazione e autorizzazione utilizzando il sito di test API Adobe](test-authn-authz-flows-using-adobes-api-test-site.md)
   + API senza client {#clientless-api}
      + [Implementazione dell&#39;API senza client - Codici di errore / Messaggi con motivo probabile / causa](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
      + [Flusso API senza client in assenza di ID dispositivo](clientless-api-flow-in-the-absence-of-device-id.md)
      + [Clientless: Evita di usare &#39;&amp;&#39;reg_code in /authenticate Request](clientless-avoid-using-reg-code-in-authenticate-request.md)
      + [Abilitazione dei servizi di adesione Primetime per un programmatore su Xbox 360 e XboxOne Clientless](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
      + [Tipo di dispositivo e metriche senza client](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
   + Esperienza utente {#user-exp}
      + [Come migrare la pagina di accesso MVPD da iFrame a popup](migr-mvpd-login-iframe-popup.md)
      + [Funzione di verifica preliminare: Come abilitare, risolvere i problemi o determinare il problema](preflight-feature.md)
   + Strumenti e utility {#tools-and-utilities}
      + [Utilizzo di Charles Proxy](using-charles-proxy.md)
   + Concetti {#concepts}
      + [Informazioni sugli ID utente](understanding-user-ids.md)
+ [Guida utente di TVE Dashboard](tve-dashboard-user-guide.md)
+ [Glossario](glossary.md)
