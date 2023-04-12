---
title: Autenticazione tramite il protocollo OAuth 2.0
description: Autenticazione tramite il protocollo OAuth 2.0
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# Autenticazione tramite il protocollo OAuth 2.0

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Sebbene SAML sia ancora il protocollo principale utilizzato per l’autenticazione dagli MVPD degli Stati Uniti e dalle imprese in generale, c’è una chiara tendenza a passare a OAuth 2.0 come protocollo di autenticazione principale. Il protocollo OAuth 2.0 (https://tools.ietf.org/html/rfc6749) è stato sviluppato principalmente per i siti di consumo ed è stato rapidamente adottato da giganti di Internet come Facebook, Google &amp; Twitter.

OAuth 2.0 ha un enorme successo e questo ha indotto le aziende a aggiornare lentamente le proprie infrastrutture per supportarlo.



## Vantaggi del passaggio a OAuth 2.0 {#adv-oauth2}

Ad alto livello, il protocollo OAuth 2.0 offre le stesse funzionalità del protocollo SAML, ma ci sono alcune distinzioni importanti.

Uno di questi è il fatto che il flusso del token di aggiornamento può essere utilizzato come un modo per aggiornare l&#39;autenticazione dietro le quinte. Questo consente all&#39;IdP (gli MVPD in questo caso) di mantenere il controllo pur consentendo comunque una buona esperienza utente, in quanto l&#39;utente non è più richiesto di effettuare l&#39;accesso spesso a causa di problemi di sicurezza.

Il protocollo offre anche una maggiore flessibilità in termini di dati esposti come provider di servizi ora può utilizzare i token per accedere ad altre API per ottenere informazioni aggiuntive. Questo a sua volta si traduce in un protocollo &quot;più chattier&quot; per i casi d’uso TVE, ma consente la flessibilità necessaria per flussi di lavoro complessi.





## Requisiti per il passaggio a OAuth 2.0 {#oauth-req}

Per supportare l’autenticazione con OAuth 2.0, un MVPD deve soddisfare i seguenti prerequisiti:

In primo luogo, l&#39;MVPD deve assicurarsi che supporti il *[Concessione del codice di autorizzazione](https://oauthlib.readthedocs.io/en/latest/oauth2/grants/authcode.html) flusso.

Dopo aver confermato che supporta il flusso, l&#39;MVPD deve fornirci le seguenti informazioni:

* punto finale di autenticazione
   * il punto finale fornirà il codice di autorizzazione che verrà successivamente utilizzato in cambio del token di aggiornamento e di accesso
* punto finale /token
   * questo fornirà il token di aggiornamento e il token di accesso
   * il token di aggiornamento deve essere stabile (non deve cambiare ogni volta che richiediamo un nuovo token di accesso)
   * l&#39;MVPD deve consentire diversi token di accesso attivi per ogni token di aggiornamento
   * questo punto finale scambia anche un token di aggiornamento per un token di accesso
* abbiamo bisogno di un **punto finale per il profilo utente**
   * questo end-point fornisce l&#39;userID, che deve essere univoco per un account e non deve contenere informazioni identificabili dalla persona
* la **/logout** punto finale (facoltativo)
   * L&#39;autenticazione Adobe Primetime reindirizza a questo punto finale, fornisce all&#39;MVPD un URI di reindirizzamento; in questo punto finale, l&#39;MVPD può cancellare i cookie sul computer client o applicare qualsiasi logica desiderata per l&#39;uscita
* è vivamente consigliato avere supporto per i client autorizzati (app client che non attivano una pagina di autorizzazione utente)
* avremo anche bisogno di:
   * **clientID** e **segreto client** per le configurazioni di integrazione
   * **tempo di vita** (TTL) valori per il token di aggiornamento e il token di accesso
   * Possiamo fornire all’MVPD un URI di callback di autorizzazione e di logout. Inoltre, se necessario, possiamo fornire agli MVPD un elenco di IP da inserire nella whitelist delle impostazioni del firewall.


## Flusso di autenticazione {#authn-flow}

Nel flusso di autenticazione, l’autenticazione Adobe Primetime comunicherà con l’MVPD sul protocollo selezionato nella configurazione. Il flusso OAuth 2.0 è rappresentato nell’immagine seguente:



![Diagramma per mostrare il flusso di autenticazione in Adobe Authentication che comunica con MVPD sul protocollo selezionato nella configurazione.](assets/authn-flow.png)

**Figura 1: Flusso di autenticazione di OAuth 2.0**



## Richiesta e risposta di autenticazione {#authn-req-response}

In breve, il flusso di autenticazione per gli MVPD che supportano il protocollo OAuth 2.0 segue questi passaggi:

1. L&#39;utente finale accede al sito del programmatore e seleziona per accedere con le sue credenziali MVPD
1. AccessEnabler installato sul lato del programmatore con invia una richiesta di autenticazione sotto forma di una richiesta HTTP all&#39;endpoint di autenticazione Adobe Primetime, che l&#39;endpoint di autenticazione Adobe Primetime reindirizzerà all&#39;endpoint di autorizzazione MVPD.
1. L’endpoint di autorizzazione MVPD invia un codice di autorizzazione all’endpoint di autenticazione Adobe Primetime
1. L’autenticazione Adobe Primetime utilizza il codice di autorizzazione ricevuto per richiedere un token di aggiornamento e un token di accesso dall’endpoint token MVPD
1. Una chiamata per recuperare informazioni utente e metadati può essere inviata all’endpoint del profilo utente nel caso in cui le informazioni utente non siano incluse nel token
1. Il token di autenticazione viene passato all’utente finale che può ora sfogliare correttamente il sito Programmer

   >[!NOTE]
   >
   >Il token di aggiornamento viene utilizzato per ottenere un nuovo token di accesso dopo che il token di accesso corrente diventa non valido o scade.


>[!IMPORTANT]
>
>Il token di aggiornamento non deve cambiare quando viene scambiato per un token di accesso.

Questa limitazione deriva dai flussi client che non consentono al server di aggiornare il token AuthNToken che, per il protocollo OAuth 2.0, contiene anche il token di aggiornamento.

Un flusso di autorizzazione tipico esegue uno scambio del token di aggiornamento salvato nel token AuthNToken per un token di accesso che viene successivamente utilizzato per eseguire la chiamata di autorizzazione nel nome dell&#39;utente autenticato inizialmente. Se il server di autorizzazione (MVPD) dovesse cambiare il token di aggiornamento e annullare la validità del token precedente, non sarà possibile aggiornare il token AuthNToken valido. Per questo motivo, gli MVPD devono supportare token di aggiornamento stabili per poter impostare integrazioni OAuth 2.0 per loro.


## Migrazione da SAML a OAuth 2.0 {#saml-auth2-migr}

La migrazione delle integrazioni da SAML a OAuth 2.0 verrà eseguita da Adobe e MVPD. Non è necessario alcun cambiamento tecnico sul lato programmatore, anche se il programmatore potrebbe voler controllare/testare il co-branding sulla pagina di accesso MVPD. Dal punto di vista dell&#39;MVPD, sono necessari gli endpoint e altre informazioni richieste nei requisiti Oauth 2.0.

Al fine di **preserve SSO**, gli utenti che dispongono già di un token di autenticazione ottenuto tramite SAML saranno comunque considerati autenticati e le loro richieste verranno instradate attraverso la vecchia integrazione SAML.

Da un punto di vista tecnico:

1. L’Adobe abiliterà un’integrazione OAuth 2.0 tra il programmatore e l’MVPD, SENZA eliminare l’integrazione SAML.
1. Dopo l’abilitazione, tutti i nuovi utenti utilizzeranno i flussi OAuth 2.0.
1. Gli utenti già autenticati, che dispongono già di un token AuthN locale che contiene l’oggetto-id SAML, verranno automaticamente instradati per Adobe tramite l’integrazione SAML.
1. Per gli utenti del passaggio 3, una volta scaduto il token AuthN generato da SAML, Adobe li tratterà come nuovi utenti e si comporterà come gli utenti nel passaggio numero 2.
1. Adobe esaminerà i pattern di utilizzo al fine di determinare il momento in cui l’integrazione SAML può essere disattivata in modo sicuro.

