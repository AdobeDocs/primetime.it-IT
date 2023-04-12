---
title: Flusso di adesione del programmatore
description: Flusso di adesione del programmatore
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---


# Flusso di adesione del programmatore {#prog-entitlement-flow}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Questo documento descrive il flusso di adesione di base dal punto di vista del programmatore.  Per informazioni sulle funzioni e sui casi d’uso oltre l’integrazione TVE di base qui descritta, consulta [Casi d&#39;uso del programmatore](/help/authentication/programmer-use-cases.md).

L&#39;autenticazione Adobe Primetime media il flusso di adesione tra programmatori e MVPD fornendo interfacce sicure e coerenti per entrambe le parti.  Dal lato del programmatore, Primetime Authentication fornisce due tipi generali di interfaccia di adesione:

1. AccessEnabler : un componente client che fornisce una libreria di API per le app sui dispositivi che possono eseguire il rendering di pagine web (ad esempio, app web, smartphone/tablet apps).
2. API Clientless: servizi web RESTful per dispositivi che non possono eseguire il rendering di pagine web (ad esempio set-top box, console giochi, smart TV). Il requisito per il rendering delle pagine web deriva dal requisito dell&#39;MVPD che gli utenti autenticano sul sito web dell&#39;MVPD.

Oltre alla panoramica neutra rispetto alla piattaforma presentata qui, è disponibile una panoramica specifica dell’API Clientless qui: Documentazione API senza client. AccessEnabler viene eseguito in modo nativo sulle piattaforme supportate (AS / JS su Web, Objective-C su iOS e Java su Android). Le API di AccessEnabler sono coerenti tra le piattaforme supportate. Tutte le piattaforme che non supportano AccessEnabler utilizzano la stessa API Clientless.

Per entrambi i tipi di interfaccia, l’autenticazione Primetime media in modo sicuro il flusso di adesione tra l’app del programmatore e l’MVPD dell’utente:

![](assets/prog-entitlement-flow.png)


*Figura: Ecosistema di autenticazione Adobe Primetime*

>[!IMPORTANT]
>
>Nel diagramma precedente c&#39;è una parte del flusso di adesione che non passa attraverso i server di autenticazione Adobe Primetime: accesso MVPD. Gli utenti devono accedere alla pagina di accesso del loro MVPD. A causa di questo requisito, sui dispositivi che non possono eseguire il rendering delle pagine web, l&#39;app del programmatore deve indirizzare gli utenti a passare a un dispositivo compatibile con il web per accedere con il proprio MVPD, dopo di che ritornano al dispositivo originale per il resto del flusso di adesione.

## Flusso di adesione {#entitlement-flow}

Ci sono quattro flussi secondari distinti che compongono il flusso di adesione di base:

1. [Flusso di avvio](/help/authentication/entitlement-flow.md#startup)
1. [Flusso di autenticazione](/help/authentication/entitlement-flow.md#authentication)
1. [Flusso di autorizzazione](/help/authentication/entitlement-flow.md#authorization)
1. [Logout FLow](/help/authentication/entitlement-flow.md#logout)

Nella visita iniziale di un utente al sito di un programmatore il flusso di adesione procede nell&#39;ordine indicato sopra. Tuttavia, nelle visite successive, a seconda che i token di autenticazione e autorizzazione siano scaduti o meno, o a seconda dei criteri di visualizzazione, un utente potrebbe attraversare solo uno o due dei flussi secondari.

### Flusso di avvio {#startup}

Stabilisce l&#39;identità del programmatore e del dispositivo, esegue le attività di inizializzazione. Questo è un prerequisito per tutte le chiamate di adesione successive.

**AccessEnabler**

* **`setRequestor()`** - Stabilisce l&#39;identificazione con AccessEnalber e, per estensione, con i server di autenticazione Adobe Primetime. Questa chiamata è un precursore del resto del flusso di adesione. Ad esempio, in JavaScript:

   ```JavaScript
     /* Define the requestor ID (Programmer/aggregator ID). */
       var requestorID = "sample_requestor_Id";
       ...
       // Callback indicating that the AccessEnabler swf has initialized
       function swfLoaded() {
           // AccessEnabler is loaded so we can use the API function it provides
           accessEnablerObject.setRequestor(requestorID); 
       ...
       }
   ```

**API senza client**

* **`\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode`** - A seconda della piattaforma, possono essere necessarie attività preliminari da eseguire prima che l’app chiami il codice di registrazione. Consulta la sezione **Documentazione API senza client** per i dettagli. Ad esempio, le piattaforme Xbox ti richiedono di completare i passaggi di sicurezza prescritti prima di richiamare regcode.

### Flusso di autenticazione {#authentication}

L’autenticazione corretta genera un token AuthN associato al dispositivo e al richiedente. L’autenticazione è un prerequisito per l’autorizzazione.

**AccessEnabler**

* `checkAuthentication()` - Controlla se esiste un token di autenticazione valido nella cache del token locale, senza attivare effettivamente il flusso di autenticazione completo. Questo attiva la `setAuthenticationStatus()` funzione di callback.
* `getAuthentication()` - Avvia il flusso di autenticazione completo. Se l’autenticazione ha esito positivo, Adobe Primetime genera un token AuthN e lo memorizza in cache sul client. L&#39;utente accede al sito MVPD selezionato, presentato in un iFrame, in una finestra a comparsa o in una visualizzazione Web, a seconda della piattaforma. Questo attiva displayProviderDialog().

**API senza client**

* `<FQDN>/.../checkauthn` - Versione del servizio Web di `checkAuthentication()` sopra.
* `<FQDN>/.../config` - Restituisce l’elenco degli MVPD nell’app a 2° schermo.
* `<FQDN>/.../authenticate` - Avvia il flusso di autenticazione dall&#39;app a 2° schermo, reindirizzando gli utenti al proprio MVPD selezionato per l&#39;accesso. Se l&#39;autenticazione Adobe Primetime ha esito positivo, genera un token AuthN e lo memorizza sul server, e l&#39;utente ritorna al dispositivo originale per completare il flusso di adesione.

Un token AuthN è considerato valido se i due punti seguenti sono veri:

* Il token AuthN non è scaduto
* L&#39;MVPD associato al token AuthN è nell&#39;elenco degli MVPD consentiti per l&#39;ID richiedente corrente

#### Flusso di lavoro di autenticazione iniziale di AccessEnabler generico {#generic-ae-initial-authn-flow}

1. L’app avvia il flusso di lavoro di autenticazione con una chiamata a `getAuthentication()`, che verifica la presenza di un token di autenticazione cache valido. Questo metodo ha un `redirectURL` parametro; se non fornisci un valore per `redirectURL`, dopo un’autenticazione riuscita, l’utente viene restituito all’URL da cui è stata inizializzata l’autenticazione.
1. AccessEnabler determina lo stato di autenticazione corrente. Se l&#39;utente è attualmente autenticato, AccessEnabler chiama il `setAuthenticationStatus()` funzione di callback, passaggio di uno stato di autenticazione che indica il successo.
1. Se l&#39;utente non è autenticato, AccessEnabler continua il flusso di autenticazione determinando se l&#39;ultimo tentativo di autenticazione dell&#39;utente ha avuto successo con un MVPD specifico. Se un ID MVPD è memorizzato nella cache E `canAuthenticate` Il flag è true OPPURE è stato selezionato un MVPD utilizzando `setSelectedProvider()`, all’utente non viene visualizzata una finestra di dialogo di selezione MVPD. Il flusso di autenticazione continua a utilizzare il valore memorizzato nella cache dell&#39;MVPD (cioè lo stesso MVPD utilizzato durante l&#39;ultima autenticazione riuscita). Viene effettuata una chiamata di rete al server back-end e l&#39;utente viene reindirizzato alla pagina di accesso MVPD.

1. Se non è presente alcun ID MVPD nella cache e non è stato selezionato alcun MVPD utilizzando `setSelectedProvider()` O `canAuthenticate` il flag è impostato su false, il `displayProviderDialog()` chiamata di callback. Questo callback indirizza l’app a creare l’interfaccia utente che presenta all’utente un elenco di MVPD tra cui scegliere. Viene fornito un array di oggetti MVPD, contenente le informazioni necessarie per creare il selettore MVPD. Ogni oggetto MVPD descrive un&#39;entità MVPD e contiene informazioni quali l&#39;ID dell&#39;MVPD e l&#39;URL in cui è possibile trovare il logo MVPD.

1. Una volta selezionato un MVPD, l&#39;app deve informare AccessEnabler della scelta dell&#39;utente. Per i client non di Flash, una volta che l&#39;utente seleziona l&#39;MVPD desiderato, si informa AccessEnabler della selezione dell&#39;utente tramite una chiamata al `setSelectedProvider()` metodo . I client di Flash inviano invece una condivisione `MVPDEvent` di tipo &quot;`mvpdSelection`&quot;, passando il provider selezionato.

1. Quando AccessEnabler viene informato della selezione MVPD dell&#39;utente, viene effettuata una chiamata di rete al server di back-end e l&#39;utente viene reindirizzato alla pagina di accesso MVPD.

1. All&#39;interno del flusso di lavoro di autenticazione, AccessEnabler comunica con l&#39;autenticazione Adobe Primetime e l&#39;MVPD selezionato per richiedere le credenziali dell&#39;utente (ID utente e password) e per verificarne l&#39;identità. Mentre alcuni MVPD reindirizzano al proprio sito per l&#39;accesso, altri richiedono di visualizzare la loro pagina di accesso all&#39;interno di un iFrame. La pagina deve includere il callback che crea un iFrame, nel caso in cui il cliente scelga uno di questi MVPD.<!-- For more information on creating a login iFrame, see  [Managing the Login IFrame](https://tve.helpdocsonline.com/managing-the-login-iframe)-->.

1. Una volta effettuato l&#39;accesso, AccessEnabler recupera il token di autenticazione e informa l&#39;app che il flusso di autenticazione è completo. AccessEnabler chiama `setAuthenticationStatus()` callback con codice di stato 1 che indica il successo. Se si verifica un errore durante l&#39;esecuzione di questi passaggi, il `setAuthenticationStatus()` il callback viene attivato con un codice di stato pari a 0 che indica un errore di autenticazione e un codice di errore corrispondente.

>[!IMPORTANT]
>Comcast è l’unico MVPD al momento che non fornisce un URL statico per il logo. I programmatori devono estrarre i loghi più recenti aggiornati da [Portale per sviluppatori XFINITY](https://developers.xfinity.com/products/tv-everywhere).

### Flusso di autorizzazione {#authorization}

L’autorizzazione è un prerequisito per la visualizzazione dei contenuti protetti. L’autorizzazione riuscita genera un token AuthZ, insieme a un Media Token di breve durata fornito all’app del programmatore a scopo di sicurezza. Tieni presente che, per supportare il flusso di lavoro di autorizzazione, devi aver eseguito in precedenza la configurazione del richiedente necessaria e aver integrato il [Verificatore token multimediale](/help/authentication/media-token-verifier-int.md). Una volta completati questi, puoi avviare l’autorizzazione.

L’app avvia l’autorizzazione quando un utente richiede l’accesso a una risorsa protetta. Trasmetti un ID risorsa specificando la risorsa richiesta (ad esempio un canale, un episodio, ecc.). La tua app verifica innanzitutto la presenza di un token di autenticazione memorizzato. Se non viene trovato, avvia il processo di autenticazione.

**AccessEnabler**

* `checkAuthorization()` - controlla l&#39;autorizzazione senza avviare il flusso di autorizzazione completo. Viene spesso utilizzato per aggiornare le informazioni sullo stato visualizzate nell’interfaccia utente dell’app Programmatore.

* `getAuthorization()` - Avvia il flusso di autorizzazione completo.

Fornisci le seguenti funzioni di callback per gestire i risultati della chiamata di autorizzazione:

* `setToken()` - Se l&#39;autenticazione ha avuto successo in precedenza e l&#39;autorizzazione ha esito positivo, AccessEnabler chiama il `setToken()` funzione di callback, passando il token multimediale di breve durata, che indica una conclusione positiva del flusso di adesione all’autenticazione Adobe Primetime. (Prima di consentire all’utente di visualizzare il contenuto protetto, l’app del programmatore controlla la validità del token multimediale utilizzando il Verificatore token multimediale.

* `tokenRequestFailed()` - Se l&#39;utente non è autorizzato per la risorsa richiesta (o se la query non riesce per altri motivi), AccessEnabler chiama questa funzione di callback (più le proprie funzioni di segnalazione errori), trasmettendo i dettagli sull&#39;errore.

**API senza client**

* `\<FQDN\>/.../authorize` - Avvia il flusso di autorizzazione completo.

#### Flusso di lavoro di autorizzazione di AccessEnabler generico {#generic-ae-authr-wf}

1. Fornire una funzione di callback che registri il GUID del programmatore assegnato con Access Enabler, utilizzando `setReqestor()`. Questa funzione di callback viene chiamata quando AccessEnabler è stato scaricato correttamente.

1. Chiamata `getAuthorization()` quando un utente richiede l’accesso a una risorsa protetta. Utilizzo `getAuthorization()`, passa un ID risorsa specificando la risorsa richiesta (ad esempio un canale, un episodio, ecc.). AccessEnabler cerca un token di autenticazione memorizzato nella cache da passare con la richiesta di autorizzazione. Se non viene trovato, avvia il flusso di autenticazione.
1. Fornire le funzioni di callback per gestire i risultati dell&#39;autorizzazione:

   * `setToken()` - Se l&#39;autorizzazione ha esito positivo o se l&#39;utente è stato precedentemente autorizzato, Access Enabler continua con il processo di autorizzazione chiamando il `setToken()` funzione di callback, passando il token di autorizzazione di breve durata.

   * `tokenRequestFailed()` - Se l&#39;utente non è autorizzato per la risorsa richiesta (o se la query non riesce per altri motivi), AccessEnabler chiama tutte le funzioni di segnalazione errori registrate, più il `tokenRequestFailed()` callback, trasmissione dei dettagli sull&#39;errore.

### Flusso di uscita {#logout}

Elimina token e altri dati associati al flusso di adesione dell&#39;utente corrente.

**AccessEnabler**

* `logout()`

**API senza client**

* `\<FQDN\>/.../logout`

## Comprendere il comportamento di AccessEnabler {#ae-behavior}

Tutte le chiamate API di AccessEnabler sono asincrone (con un’eccezione, indicata nei riferimenti API). È possibile chiamare un’API un numero arbitrario di volte, tuttavia non esiste una forte garanzia che le azioni attivate dalle chiamate vengano completate nello stesso ordine in cui sono state effettuate. (Un&#39;eccezione a questo è il runtime di Flash Player corrente; senza multi-thread, le chiamate *fare* completa nell&#39;ordine in cui vengono chiamati.)

Per distinguere tra le risposte e poter associare le risposte alle chiamate, tutti i callback richiamano i parametri di input. Ciò include `setToken()` e`tokenRequestFailed()`, che in ultima analisi viene attivata da `checkAuthorization()`. (Per `checkAuthorization()` callback, la risorsa utilizzata viene riportata di nuovo). Sfruttando questa funzione, puoi distinguere quale risposta corrisponde a quale chiamata. Per utilizzare questa funzione è possibile codificare qualcosa di simile al seguente:

```JavaScript
    for each (resource in ["TNT", "CNN", "TBS", "AdultSwim"] ) {
         ae.checkAuthorization(resource);
    }
    
    // Success callback
    function setToken(resource, token) {
         // Use "resource" to figure 
         // out which checkAuthorization
         // call triggered this response
    }
    
    // Old error callback
    function tokenRequestFailed(resource, error, details) {
         // use "resource" to figure
         // out in response to which
         // checkAuthorization call
         // this was triggered
    }
    
    // Error callback using new error api
    ae.bind("errorEvent',"errorHandler");
    
    function errorHandler(error) {
         if(error.resource) {        
              // Use error.resource to figure
              // which checkAuthorization call
              // triggered this response
         }
    }
```

### Domande frequenti sul comportamento AEM {#ae-beh-faq}

**Domanda. Cosa succede se effettuo una seconda chiamata AccessEnabler prima del termine della prima chiamata?**

La prima chiamata continua a essere eseguita durante l’esecuzione della seconda chiamata (comunicazioni asincrone).

**Domanda. È disponibile un numero massimo di chiamate simultanee supportate da AccessEnabler?**

Nessun limite è impostato esplicitamente nel codice di AccessEnabler, in modo da essere limitati solo dalle risorse di sistema disponibili, nonché dalla capacità dell&#39;MVPD.

<!--

>[!MORELIKETHIS]
>
>*   [Programmer use cases](/help/authentication/programmer-use-cases.md)
>*   Error Reporting
>**Platform Cookbooks:**
>*   Clientless integration cookbook
>*   iOS Integration Cookbook
>*   Android Integration Cookbook
>*   JavaScript Integration Cookbook
>*   ActionScript Integration Cookbook
>*   Windows 8 Integration Cookbook
>*   AIR Native Extension Overview
-->