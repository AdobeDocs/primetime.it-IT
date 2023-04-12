---
title: Guida di riferimento rapido per iOS/tvOS
description: Guida di riferimento rapido per iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# Guida di riferimento rapido per l&#39;SDK di iOS/tvOS {#iostvos-sdk-cookbook}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro}

Questo documento descrive i flussi di lavoro di adesione che un&#39;applicazione di livello superiore di un programmatore può implementare attraverso le API esposte dalla libreria AccessEnabler iOS/tvOS.

La soluzione di adesione all&#39;autenticazione Adobe Primetime per iOS/tvOS è in ultima analisi suddivisa in due domini:

* Dominio dell&#39;interfaccia utente : si tratta del livello di applicazione superiore che implementa l&#39;interfaccia utente e utilizza i servizi forniti dalla libreria AccessEnabler per fornire accesso ai contenuti con restrizioni.

* Dominio AccessEnabler : in questo punto i flussi di lavoro di adesione vengono implementati sotto forma di:

   * Chiamate di rete effettuate ai server back-end di Adobe
   * Regole business-logic relative ai flussi di lavoro di autenticazione e autorizzazione
   * Gestione di varie risorse ed elaborazione dello stato del flusso di lavoro (come la cache dei token)

L&#39;obiettivo del dominio AccessEnabler è quello di nascondere tutte le complessità dei flussi di lavoro di adesione e fornire all&#39;applicazione di livello superiore (tramite la libreria AccessEnabler) un set di primitivi di adesione semplici con cui implementare i flussi di lavoro di adesione:

1. Imposta l&#39;identità del richiedente
1. Controllare e ottenere l&#39;autenticazione con un provider di identità specifico
1. Controllare e ottenere l&#39;autorizzazione per una particolare risorsa
1. Logout
1. Flussi SSO di Apple propagando il framework VSA di Apple

L&#39;attività di rete di AccessEnabler ha luogo nel proprio thread, pertanto il thread di interfaccia utente non viene mai bloccato. Di conseguenza, il canale di comunicazione bidirezionale tra i due domini di applicazione deve seguire un pattern completamente asincrono:

* Il livello dell&#39;applicazione dell&#39;interfaccia utente invia messaggi al dominio AccessEnabler tramite le chiamate API esposte dalla libreria AccessEnabler.
* AccessEnabler risponde al livello dell&#39;interfaccia utente attraverso i metodi di callback inclusi nel protocollo AccessEnabler che il livello dell&#39;interfaccia utente registra con la libreria AccessEnabler.

## Configurazione dell’ID visitatore {#visitorIDSetup}

Configurazione di un [Marketing Cloud visitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) dal punto di vista dell’analisi, il valore è molto importante. Una volta impostato il valore visitorID, l&#39;SDK invierà queste informazioni insieme a tutte le chiamate di rete e il server di autenticazione di Adobe Primetime raccoglierà queste informazioni. In futuro sarà possibile correlare le analisi del servizio di autenticazione di Adobe Primetime con qualsiasi altro rapporto di analisi disponibile da altre applicazioni o siti web. Informazioni su come impostare visitorID sono disponibili [qui](#setOptions).

## Flussi di diritto {#entitlement}

A.  [Prerequisiti](#prereqs) </br>
B.  [Flusso di avvio](#startup_flow) </br>
C.  [Flusso di autenticazione con Apple SSO](#authn_flow_wo_applesso)  </br>
D.  [Flusso di autenticazione con Apple SSO su iOS](#authn_flow_with_applesso) </br>
E.  [Flusso di autenticazione con Apple SSO su tvOS](#authn_flow_with_applesso_tvOS) </br>
F.  [Flusso di autorizzazione](#authz_flow) </br>
G.  [Visualizza flusso multimediale](#media_flow) </br>
H.  [Flusso di disconnessione senza Apple SSO](#logout_flow_wo_AppleSSO) </br>
I.  [Flusso di disconnessione con Apple SSO](#logout_flow_with_AppleSSO) </br>


### A. Prerequisiti {#prereqs}

1. Crea le funzioni di callback:
   * `setRequestorComplete()` </br>
   * Attivato da [setRequestor()](#$setReq), restituisce successo o errore. </br>
   * Il successo indica che è possibile procedere con le chiamate di adesione.

   * [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      * Attivato da [`getAuthentication()`](#$getAuthN) solo se l&#39;utente non ha selezionato un provider (MVPD) e non è ancora autenticato. </br>
      * La `mvpds` è un array dei provider disponibili per l&#39;utente.
   * `setAuthenticationStatus(status, errorcode)` </br>
      * Attivato da `checkAuthentication()` ogni volta. </br>
      * Attivato da [`getAuthentication()`](#$getAuthN) solo se l&#39;utente è già autenticato e ha selezionato un provider. </br>
      * Lo stato restituito è riuscito o non riuscito. Il codice di errore descrive il tipo di errore.
   * [`navigateToUrl(url)`](#$nav2url) </br>
      * Attivato da [`getAuthentication()`](#$getAuthN) dopo che l&#39;utente ha selezionato un MVPD. La `url` fornisce la posizione della pagina di login di MVPD.
   * `sendTrackingData(event, data)` </br>
      * Attivato da `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.
      * La `event` il parametro indica l&#39;evento di adesione che si è verificato; la `data` è un elenco di valori relativi all&#39;evento. 
   * `setToken(token, resource)`

      * Attivato da [checkAuthorization()](#checkAuthZ) e [getAuthorization()](#$getAuthZ) dopo aver ottenuto l’autorizzazione per visualizzare una risorsa.
      * La `token` parametro è il token multimediale di breve durata; la `resource` è il contenuto che l&#39;utente è autorizzato a visualizzare.
   * `tokenRequestFailed(resource, code, description)` </br>
      * Attivato da [checkAuthorization()](#checkAuthZ) e [getAuthorization()](#$getAuthZ) dopo un&#39;autorizzazione non riuscita.
      * La `resource` parametro è il contenuto che l&#39;utente stava tentando di visualizzare; la `code` parametro è il codice di errore che indica il tipo di errore verificatosi; la `description` Il parametro descrive l&#39;errore associato al codice di errore.
   * `selectedProvider(mvpd)` </br>
      * Attivato da [`getSelectedProvider()`](#getSelProv).
      * La `mvpd` fornisce informazioni sul provider selezionato dall&#39;utente.
   * `setMetadataStatus(metadata, key, arguments)`
      * Attivato da `getMetadata().`
      * La `metadata` fornisce i dati specifici richiesti; la `key` è la chiave utilizzata nel [getMetadata()](#getMeta) richiesta; e `arguments` è lo stesso dizionario passato a [getMetadata()](#getMeta).
   * [`preauthorizedResources(authorizedResources)`](#preauthResources)

      * Attivato da [`checkPreauthorizedResources()`](#checkPreauth).

      * La `authorizedResources` presenta le risorse che l&#39;utente è autorizzato a visualizzare.
   * [`currentTvProviderDialog(viewController)`](#presentTvDialog)

      * Attivato da [getAuthentication()](#getAuthN) quando il richiedente corrente supporta almeno su MVPD con supporto SSO.
      * Il parametro viewController è la finestra di dialogo SSO di Apple e deve essere presentato sul controller della vista principale.
   * [`dismissTvProviderDialog(viewController)`](#dismissTvDialog)

      * Attivazione da un&#39;azione dell&#39;utente (selezionando &quot;Annulla&quot; o &quot;Altri fornitori TV&quot; dalla finestra di dialogo SSO di Apple).
      * Il parametro viewController è la finestra di dialogo SSO di Apple e deve essere ignorato dal controller di visualizzazione principale.











![](assets/iOS-flows.png)

### B. Flusso di avvio {#startup_flow}

1. Avvia l&#39;applicazione di livello superiore.</br>
1. Avvia autenticazione Adobe Primetime </br>

   a) Chiamata [`init`](#$init) per creare una singola istanza di Adobe Primetime authentication AccessEnabler.
   * **Dipendenza:** Libreria nativa iOS/tvOS di autenticazione Adobe Primetime (AccessEnabler)
   b) Chiamata `setRequestor()` stabilire l&#39;identità del programmatore; trasmettere il `requestorID` e (facoltativamente) un array di endpoint di autenticazione Adobe Primetime. Per tvOS dovrai anche fornire la chiave pubblica e il segreto. Vedi [Documentazione senza client](#create_dev) per i dettagli.

   * **Dipendenza:** RequestorID di autenticazione di Adobe Primetime valido (puoi utilizzare Adobe Primetime Authentication Account Manager per organizzare questa operazione).

   * **Triggers:**
      [setRequestorComplete()](#$setReqComplete) callback.
   >[!NOTE]
   >
   >Non è possibile completare nessuna richiesta di adesione finché il richiedente non ha stabilito completamente l&#39;identità. Ciò significa in effetti che mentre [`setRequestor()`](#$setReq)  è ancora in esecuzione, tutte le richieste di adesione successive. Ad esempio: [`checkAuthentication()`](#checkAuthN) sono bloccati.

   Sono disponibili due opzioni di implementazione: Una volta inviate le informazioni di identificazione del richiedente al server di back-end, il livello di applicazione dell&#39;interfaccia utente può scegliere uno dei due approcci seguenti: </br>

   1. Attendi l&#39;attivazione della [`setRequestorComplete()`](#setReqComplete) callback (parte del delegato di AccessEnabler). Questa opzione offre la massima certezza che [`setRequestor()`](#$setReq) completato, quindi consigliato per la maggior parte delle implementazioni.

   1. Continua senza attendere l&#39;attivazione del [`setRequestorComplete()`](#setReqComplete) callback e avvio dell&#39;emissione di richieste di adesione. Queste chiamate (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) vengono messe in coda dalla libreria AccessEnabler, che effettuerà le chiamate di rete effettive dopo il [`setRequestor()`](#$setReq). Questa opzione può essere interrotta occasionalmente se, ad esempio, la connessione di rete è instabile.



1. Chiamata `checkAuthentication()` per verificare l&#39;esistenza di un&#39;autenticazione senza avviare il flusso completo di autenticazione.  Se questa chiamata ha esito positivo, puoi procedere direttamente al flusso Autorizzazione. In caso contrario, procedi al flusso di autenticazione.

   * **Dipendenza:** Chiamata riuscita a [setRequestor()](#$setReq) (questa dipendenza si applica anche a tutte le chiamate successive).

   * **Triggers:** [setAuthenticationStatus()](#$setAuthNStatus) callback.


### C. Flusso di autenticazione senza Apple SSO {#authn_flow_wo_applesso}

1. Chiamata [`getAuthentication()`](#$getAuthN) per avviare il flusso di autenticazione o per ottenere la conferma che l’utente è già autenticato.

   **Triggers:**

   * La [setAuthenticationStatus()](#$setAuthNStatus) callback, se l&#39;utente è già autenticato. In questo caso, procedi direttamente al [Flusso di autorizzazione](#authz_flow).

   * La [displayProviderDialog()](#$dispProvDialog) callback, se l&#39;utente non è ancora autenticato.

1. Presentare all’utente l’elenco dei provider inviati a
   [`displayProviderDialog()`](#dispProvDialog).

1. Dopo che l&#39;utente seleziona un provider, ottieni l&#39;URL dell&#39;MVPD dell&#39;utente dal `navigateToUrl:` o `navigateToUrl:useSVC:` callback e apri un `UIWebView/WKWebView` o `SFSafariViewController` e indirizza il controller all&#39;URL.

1. Attraverso il `UIWebView/WKWebView` o `SFSafariViewController` creata nel passaggio precedente, l&#39;utente arriva alla pagina di accesso dell&#39;MVPD e immette le credenziali di accesso. Diverse operazioni di reindirizzamento si svolgono all&#39;interno del controller.</br>

>[!NOTE]
>
>A questo punto, l&#39;utente ha l&#39;opportunità di annullare il flusso di autenticazione. In questo caso, il livello dell&#39;interfaccia utente deve informare AccessEnabler di questo evento chiamando [setSelectedProvider()](#setSelProv) con `null` come parametro. Questo consente ad AccessEnabler di ripulire il proprio stato interno e reimpostare il flusso di autenticazione.

1. Dopo l’accesso dell’utente, il livello dell’applicazione rileva il caricamento di un URL personalizzato specifico. Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che il flusso di autenticazione è stato completato e che è sicuro chiudere il `UIWebView/WKWebView` o `SFSafariViewController` controller. Nel caso in cui `SFSafariViewController`è necessario utilizzare il controller . L&#39;URL personalizzato specifico è definito dalla **`application's custom scheme`** (ad esempio`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), altrimenti questo URL personalizzato specifico viene definito dalla **`ADOBEPASS_REDIRECT_URL`** costante (ovvero `adobepass://ios.app`).

1. Chiudi il controller UIWebView/WKWebView o SFSafariViewController e chiama il controller AccessEnabler `handleExternalURL:url` Metodo API, che indica ad AccessEnabler di recuperare il token di autenticazione dal server back-end.

1. (Facoltativo) Chiama [`checkPreauthorizedResources(resources)`](#$checkPreauth) per verificare quali risorse l’utente è autorizzato a visualizzare. La `resources` è un array di risorse protette associato al token di autenticazione dell&#39;utente. Un utilizzo delle informazioni di autorizzazione ottenute dall’MVPD dell’utente consiste nel decorare l’interfaccia utente (ad esempio, simboli bloccati/sbloccati accanto al contenuto protetto).

   * **Triggers:** [`preauthorizedResources()`](#preauthResources) callback
   * **Punto di esecuzione:** Dopo il flusso di autenticazione completato

1. Se l’autenticazione ha avuto esito positivo, procedi al flusso di autorizzazione.

### D. Flusso di autenticazione con Apple SSO su iOS {#authn_flow_with_applesso}

1. Chiamata [`getAuthentication()`](#$getAuthN) per avviare il flusso di autenticazione o per ottenere la conferma che l’utente è già autenticato.
   **Triggers:**

   * La [presentTvProviderDialog()](#presentTvDialog) callback, se l&#39;utente non è autenticato e il richiedente corrente ha almeno su MVPD che supporta SSO. Se nessun MVPD supporta SSO, verrà utilizzato il flusso di autenticazione classico.

1. Dopo che l&#39;utente seleziona un provider, la libreria AccessEnabler ottiene un token di autenticazione con le informazioni fornite dal framework VSA di Apple.

1. La [setAuthenticationsStatus()](#setAuthNStatus) viene attivato il callback. A questo punto l&#39;utente deve essere autenticato con Apple SSO.

1. [Facoltativo] Chiamata [`checkPreauthorizedResources(resources)`](#$checkPreauth) per verificare quali risorse l’utente è autorizzato a visualizzare. La `resources` è un array di risorse protette associato al token di autenticazione dell&#39;utente. Un utilizzo delle informazioni di autorizzazione ottenute dall’MVPD dell’utente consiste nel decorare l’interfaccia utente (ad esempio, simboli bloccati/sbloccati accanto al contenuto protetto).

   * **Triggers:** [`preauthorizedResources()`](#preauthResources) callback
   * **Punto di esecuzione:** Dopo il flusso di autenticazione completato

1. Se l’autenticazione ha avuto esito positivo, procedi al flusso di autorizzazione.

### E. Flusso di autenticazione con Apple SSO su tvOS {#authn_flow_with_applesso_tvOS}

1. Chiamata [`getAuthentication()`](#$getAuthN) per avviare il flusso di autenticazione o per ottenere la conferma che l’utente è già autenticato.
   **Triggers:**
   * La [`presentTvProviderDialog()`](#presentTvDialog) callback, se l&#39;utente non è autenticato e il richiedente corrente ha almeno su MVPD che supporta SSO. Se nessun MVPD supporta SSO, verrà utilizzato il flusso di autenticazione classico.

1. Dopo che l&#39;utente seleziona un provider [`status()`](#status_callback_implementation) verrà chiamato il callback. Verrà fornito un codice di registrazione e la libreria AccessEnabler avvierà il polling del server per un&#39;autenticazione a seconda schermata corretta.

1. Se il codice di registrazione fornito è stato utilizzato per autenticare correttamente nella seconda schermata, la [`setAuthenticatiosStatus()`](#setAuthNStatus) viene attivato il callback. A questo punto l&#39;utente deve essere autenticato con Apple SSO.
1. [Facoltativo] Chiamata [`checkPreauthorizedResources(resources)`](#$checkPreauth) per verificare quali risorse l’utente è autorizzato a visualizzare. La `resources` è un array di risorse protette associato al token di autenticazione dell&#39;utente. Un utilizzo delle informazioni di autorizzazione ottenute dall’MVPD dell’utente consiste nel decorare l’interfaccia utente (ad esempio, simboli bloccati/sbloccati accanto al contenuto protetto).

   * **Triggers:** [`preauthorizedResources()`](#preauthResources) callback

   * **Punto di esecuzione:** Dopo il flusso di autenticazione completato
1. Se l’autenticazione ha avuto esito positivo, procedi al flusso di autorizzazione.

### F. Flusso di autorizzazione {#authz_flow}

1. Chiamata [getAuthorization()](#$getAuthZ) avviare il flusso di autorizzazione.

   * **Dipendenza:** ResourceID(s) valido(i) concordato con l&#39;MVPD(s).
   * Gli ID risorsa devono essere gli stessi utilizzati su qualsiasi altro dispositivo o piattaforma e devono essere gli stessi negli MVPD. Per informazioni sugli ID risorsa, vedi [Identificazione delle risorse protette](/help/authentication/identify-protected-resources.md)

1. Convalida autenticazione e autorizzazione.

   * Se la [getAuthorization()](#$getAuthZ) la chiamata ha esito positivo: L’utente dispone di token AuthN e AuthZ validi (l’utente è autenticato e autorizzato a guardare il supporto richiesto).

   * Se [getAuthorization()](#$getAuthZ) errore: Esamina l’eccezione generata per determinare il relativo tipo (AuthN, AuthZ o altro):
      * Se si è verificato un errore di autenticazione (AuthN), riavvia il flusso di autenticazione.
      * Se si è verificato un errore di autorizzazione (AuthZ), l’utente non è autorizzato a guardare il supporto richiesto e deve essere visualizzato un messaggio di errore di qualche tipo.
      * Se si è verificato un altro tipo di errore (errore di connessione, errore di rete, ecc.) quindi mostrare all’utente un messaggio di errore appropriato.

1. Convalida il token per contenuti multimediali brevi.\
   Utilizza la libreria Adobe Primetime authentication Media Token Verifier per verificare il token multimediale di breve durata restituito dal [getAuthorization()](#$getAuthZ) chiama qui sopra:

   * Se la convalida ha esito positivo: Riprodurre il supporto richiesto per l&#39;utente.
   * Se la convalida non riesce: Il token AuthZ non è valido. La richiesta multimediale deve essere rifiutata e deve essere visualizzato un messaggio di errore all&#39;utente.


1. Torna al normale flusso di applicazioni.

### G. Visualizza flusso multimediale {#media_flow}

1. L&#39;utente seleziona il supporto da visualizzare.
1. I media sono protetti? L&#39;applicazione controlla se il supporto selezionato è protetto:

   * Se il supporto selezionato è protetto, l&#39;applicazione avvia la [Flusso di autorizzazione](#authz_flow) sopra.

   * Se il supporto selezionato non è protetto, riprodurlo per l&#39;utente.

### H. Flusso di disconnessione senza Apple SSO {#logout_flow_wo_AppleSSO}

1. Chiamata [`logout()`](#$logout) per disconnettersi dall&#39;utente. AccessEnabler cancella tutti i valori e i token memorizzati nella cache. Dopo aver cancellato la cache, AccessEnabler effettua una chiamata al server per pulire le sessioni lato server. Tieni presente che, poiché la chiamata al server potrebbe causare un reindirizzamento SAML all’IdP (questo consente la pulizia della sessione sul lato IdP), questa chiamata deve seguire tutti i reindirizzamenti. Per questo motivo, questa chiamata deve essere gestita all&#39;interno di un controller UIWebView/WKWebView o SFSafariViewController.

   a) Seguendo lo stesso pattern del flusso di lavoro di autenticazione, il dominio AccessEnabler invia una richiesta al livello dell’applicazione dell’interfaccia utente tramite il `navigateToUrl:` o `navigateToUrl:useSVC:` callback, per creare un controller UIWebView/WKWebView o SFSafariViewController e per istruire il caricamento dell&#39;URL fornito nel callback `url` parametro . Si tratta dell’URL dell’endpoint di logout sul server back-end.

   b) L&#39;applicazione deve monitorare l&#39;attività del `UIWebView/WKWebView or SFSafariViewController` controlla e rileva il momento in cui carica un URL personalizzato specifico, in quanto attraversa diversi reindirizzamenti. Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che il flusso di logout è stato completato e che è sicuro chiudere il `UIWebView/WKWebView` o `SFSafariViewController` controller. Quando il controller carica questo URL personalizzato specifico, l&#39;applicazione deve chiudere la `UIWebView/WKWebView or SFSafariViewController` controller e chiamata di AccessEnabler `handleExternalURL:url`Metodo API. Nel caso in cui `SFSafariViewController`è necessario utilizzare il controller . L&#39;URL personalizzato specifico è definito dalla **`application's custom scheme`** (ad esempio, `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), altrimenti questo URL personalizzato specifico viene definito dalla **`ADOBEPASS_REDIRECT_URL`**  costante (ovvero `adobepass://ios.app`).

   >[!NOTE]
   >
   >Il flusso di logout è diverso dal flusso di autenticazione in quanto l’utente non è tenuto a interagire in alcun modo con UIWebView/WKWebView o SFSafariViewController. Il livello dell&#39;applicazione dell&#39;interfaccia utente utilizza un UIWebView/WKWebView o SFSafariViewController per assicurarsi che tutti i reindirizzamenti siano seguiti. Pertanto, è possibile (e consigliato) rendere invisibile il controller (cioè nascosto) durante il processo di logout.


### I. Flusso di disconnessione con Apple SSO {#logout_flow_with_AppleSSO}

1. Chiamata [`logout()`](#$logout) per disconnettersi dall&#39;utente.
1. La [status()](#status_callback_implementation) il callback verrà chiamato con id VSA203.
1. All&#39;utente deve essere richiesto di effettuare l&#39;accesso anche dalle impostazioni di sistema. In caso contrario, al riavvio dell’applicazione si verificherà una nuova autenticazione.



<!--
### Related Information {#related}


- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note)](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->