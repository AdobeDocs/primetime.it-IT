---
title: Riferimento API SDK JavaScript
description: Riferimento API SDK JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# Riferimento API SDK JavaScript {#javascript-sdk-api-reference}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Riferimento API {#api-reference}

Queste funzioni avviano richieste di interazione con un MVPD. Tutte le chiamate sono asincrone; devi implementare [callback](#callbacks) per gestire le risposte:

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor (inRequestorID, endpoint, opzioni){#setrequestor(inRequestorID,endpoints,options)}

**Descrizione:** Identifica il sito da cui provengono le richieste.  Devi effettuare questa chiamata prima di qualsiasi altra chiamata API in una sessione di comunicazione. 

**Parametri:**

- *inRequestorID* - l&#39;identificativo univoco assegnato al sito di origine durante la registrazione.

- *endpoint* - Questo parametro è facoltativo. Può essere uno dei seguenti valori:

   - Array che consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). Se vengono forniti più URL, l’elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al fornitore di servizi più veloce; cioè, il fornitore che ha risposto per primo e che supporta quel MVPD. Per impostazione predefinita (se non è specificato alcun valore), viene utilizzato il provider di servizi Adobe (<http://sp.auth.adobe.com/>).

   Esempio:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *options* - Un oggetto JSON contenente il valore ID applicazione, le impostazioni di aggiornamento del valore ID visitatore (logout accesso in background) e le impostazioni MVPD (iFrame). Tutti i valori sono facoltativi.
   1. Se specificato, l&#39;Experience Cloud visitorID viene segnalato per tutte le chiamate di rete eseguite dalla libreria . Il valore può essere successivamente utilizzato per i rapporti di analisi avanzati.
   2. Se è specificato l&#39;identificatore univoco dell&#39;applicazione -`applicationId` - il valore verrà aggiunto a tutte le chiamate successive effettuate dall&#39;applicazione come parte dell&#39;intestazione HTTP X-Device-Info. Questo valore può essere recuperato in un secondo momento da [ESM](/help/authentication/entitlement-service-monitoring-overview.md) rapporti utilizzando la query corretta.

   **Nota:** Tutte le chiavi JSON fanno distinzione tra maiuscole e minuscole.

    Esempio:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- Il programmatore può ignorare le impostazioni MVPD configurate nell&#39;autenticazione Adobe Primetime, specificando se è necessario o meno un iFrame per l&#39;accesso (*iFrameObbligatorio* key) e le dimensioni iFrame (*iFrameWidth* e *iFrameHeight* tasti). L&#39;oggetto JSON ha il seguente modello:

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```
 

Tutte le chiavi di livello superiore nel modello precedente sono facoltative e hanno valori predefiniti (*backgroundLogin*, *backgroundLogut* sono false per impostazione predefinita e mvpdConfig è null - significa che nessuna impostazione MVPD è ignorata.

 
- **Nota**: Specificando valori/tipi non validi per i parametri di cui sopra si otterrà un comportamento non definito.

 

Ecco un esempio di configurazione per lo scenario seguente: attivazione dell&#39;accesso e del logout senza aggiornamento, modifica di MVPD1 in accesso con reindirizzamento a pagina intera (non-iFrame) e da MVPD2 a iFrame con larghezza=500 e altezza=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**Callback attivato:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[Torna all&#39;inizio](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**Descrizione:** Richiede l’autorizzazione per la risorsa specificata. Ogni volta che un cliente tenta di accedere a una risorsa autorizzabile, chiama questa funzione per ottenere un token di autorizzazione di breve durata da Access Enabler. Gli ID risorsa sono concordati con l&#39;MVPD che fornisce l&#39;autorizzazione.

Utilizza il token di autenticazione memorizzato nella cache per il cliente corrente. Se non viene trovato alcun token, avvia prima il processo di autenticazione, quindi continua con l&#39;autorizzazione.\
 
**Parametri:**

- `inResourceID` - L&#39;ID della risorsa per la quale l&#39;utente richiede l&#39;autorizzazione.
- `redirect_url` - Se necessario, fornisci un URL di reindirizzamento, in modo che il processo di autorizzazione dell&#39;MVPD restituisca l&#39;utente a quella pagina anziché alla pagina da cui è stata avviata l&#39;autorizzazione.


**Callback attivato:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) sul successo, [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) in caso di guasto

>[!CAUTION]
>
>Utilizza checkAuthorization() invece di getAuthorization() quando possibile. Il metodo getAuthorization() avvia un flusso di autenticazione completo (se l’utente non è autenticato) che potrebbe comportare un’implementazione complicata da parte del programmatore.

</b>

[Torna all&#39;inizio](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**Descrizione:** Richiede l’autenticazione per il cliente corrente. Generalmente chiamato in risposta a un clic su un pulsante di accesso. Verifica la presenza di un token di autenticazione memorizzato nella cache per il cliente corrente. Se non viene trovato alcun token, avvia il processo di autenticazione. Viene richiamata la finestra di dialogo di selezione del provider predefinito o personalizzato, quindi viene utilizzato il provider selezionato per reindirizzare all&#39;interfaccia di accesso di MVPD.

In caso di esito positivo, crea e memorizza un token di autenticazione per l’utente. Se l&#39;autenticazione non riesce, il provider restituisce un messaggio di errore appropriato al tuo [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) callback.

**Parametri:**

- redirect_url : fornisce facoltativamente un URL di reindirizzamento, in modo che il processo di autenticazione dell’MVPD restituisca l’utente a quella pagina anziché alla pagina da cui è stata avviata l’autenticazione.

 **Callback attivato:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Torna all&#39;inizio](#top)

</br>

## checkAuthN {#checkauthn}

**Descrizione:** Controlla lo stato di autenticazione corrente per il cliente corrente.  Non associata ad alcuna interfaccia utente.

**Callback attivato:** [setAuthentationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[Torna all&#39;inizio](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per controllare lo stato di autorizzazione per il cliente corrente e la risorsa specificata. Inizia controllando prima lo stato di autenticazione. Se non è autenticato, viene attivato il callback tokenRequestFailed() e il metodo esce. Se l&#39;utente è autenticato, attiva anche il flusso di autorizzazione. Vedi i dettagli [getAuthorization()](#getAuthZ metodo .

>[!TIP]
>
> **Utilizzo delle funzioni di controllo-stato**  Non è necessario controllare lo stato dell&#39;autenticazione o dell&#39;autorizzazione prima di richiedere l&#39;autorizzazione. È possibile chiamare queste funzioni, ad esempio, per aggiornare la visualizzazione dello stato. Non utilizzarli quando è necessaria un’interazione con l’utente.

**Parametri:**

- `inResourceID` - L&#39;ID della risorsa per la quale l&#39;utente richiede l&#39;autorizzazione.

 
**Callback attivato:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**Descrizione:** Richiede lo stato di autorizzazione &quot;preflight&quot; per un elenco di risorse.

**Parametri:**

- *risorse*: Il parametro resources è una matrice di risorse per le quali è necessario controllare l&#39;autorizzazione. Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa nel `getAuthorization()` Chiamare, cioè, è un valore concordato stabilito tra il programmatore e il MVPD, o un frammento RSS media. 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

Questa variante API è disponibile a partire dalla versione SDK 4.0 di JS


**Parametri:**

- *risorse*: Il parametro resources è una matrice di risorse per le quali è necessario controllare l&#39;autorizzazione. Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa nel `getAuthorization()` Chiamare, cioè, è un valore concordato stabilito tra il programmatore e il MVPD, o un frammento RSS media. 

- *cache*: Utilizzare la cache interna durante il controllo delle risorse preautorizzate. Si tratta di un parametro facoltativo, con impostazione predefinita su **true**. Se true il comportamento è identico all’API di cui sopra, il che significa che le chiamate successive a questa funzione utilizzeranno una cache interna per risolvere la risorsa preautorizzata. Passaggio **false** per questo parametro disabiliterà la cache interna, dando luogo a una chiamata al server ogni volta che il **checkPreauthorizedResources** Si chiama API .

**Callback attivato:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[Torna all&#39;inizio](#top)
</br>

## getMetadata(Key) {#getMetadata}

**Descrizione:** Recupera le informazioni esposte come metadati dalla libreria di Access Enabler.

Esistono due tipi di metadati: 

- **Statico** (token di autenticazione TTL, token di autorizzazione TTL e ID dispositivo) 
- **Metadati utente** (Questo include informazioni specifiche per l&#39;utente che vengono trasmesse dall&#39;MVPD al dispositivo dell&#39;utente durante i flussi di autenticazione e/o autorizzazione)

**Ulteriori informazioni:** [Metadati utente](#UserMetadata)

**Parametri:**

- *key*: ID che specifica i metadati richiesti:
   - Se la chiave è `"TTL_AUTHN",` quindi viene eseguita la query per ottenere il tempo di scadenza del token di autenticazione.

   - Se la chiave è `"TTL_AUTHZ"` e params è una matrice contenente l’ID risorsa come stringa, quindi la query viene eseguita per ottenere il tempo di scadenza del token di autorizzazione associato alla risorsa specificata.

   - Se la chiave è `"DEVICEID"` quindi viene eseguita la query per ottenere l&#39;id dispositivo corrente. Tieni presente che questa funzione è disabilitata per impostazione predefinita e che i programmatori devono contattare l’Adobe per informazioni relative all’abilitazione e alle tariffe.

   - Se la chiave proviene dal seguente elenco di tipi di metadati utente, un oggetto JSON contenente i metadati utente corrispondenti viene inviato al [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) funzione di callback:

   - `"zip"` - Codice postale

   - `"encryptedZip"` - Codice postale crittografato

   - `"householdID"` - identificatore della famiglia. Nel caso in cui un MVPD non supporti i sottoaccount, questo sarà identico a userID.

   - `"maxRating"` - Valutazione massima per i genitori dell&#39;utente

   - `"userID"` - Identificatore utente. Nel caso in cui un MVPD supporti i conti secondari e l&#39;utente non sia l&#39;account principale, userID sarà diverso da familyID.

   - `"channelID"` - Elenco dei canali che l&#39;utente ha diritto di visualizzare

   - `"is_hoh"` - Flag che identifica se un utente è a capo della famiglia

   - `"encryptedZip"` - Codice postale crittografato

   - `"typeID"` - Flag che identifica se l&#39;account utente è principale/secondario

   - `"primaryOID"` - Identificativo della famiglia

   - `"postalCode"` - Simile al codice postale

   - `"acctID"` - ID account

   - `"acctParentID"` - ID padre account
   **Nota**: I metadati utente effettivi disponibili per un programmatore dipendono da ciò che un MVPD rende disponibile.  Vedi [Metadati utente](#UserMetadata) per l’elenco corrente dei metadati utente disponibili.


Ad esempio:

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```
 

**Callback attivato:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[Torna all&#39;inizio](#top)

</br>


## setSelectedProvider(providerID) {#setSelectedProvider}

**Descrizione:** Chiama questa funzione quando l&#39;utente ha selezionato un MVPD dall&#39;interfaccia utente di selezione del provider per inviare la selezione del provider ad Access Enabler o chiamare questa funzione con un parametro null nel caso in cui l&#39;utente abbia saltato l&#39;interfaccia utente di selezione del provider senza selezionare un provider. 

**Callback attivato:**[ setAuthentationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Torna all&#39;inizio](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**Descrizione:** Recupera i risultati della selezione del cliente nella finestra di dialogo di selezione del provider. Questo può essere utilizzato in qualsiasi momento dopo il controllo di autenticazione iniziale.

Questa funzione è asincrona e restituisce il suo risultato al tuo `selectedProvider()` funzione di callback.

- **MVPD** MVPD attualmente selezionato o nullo se non è stato selezionato alcun MVPD.
- **AE_State** Il risultato dell&#39;autenticazione per il cliente corrente: &quot;Nuovo utente&quot;, &quot;Utente non autenticato&quot; o &quot;Utente autenticato&quot;

 **Callback attivato:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[Torna all&#39;inizio](#top)

</br>

## disconnessione {#logout}

**Descrizione:** Disconnette il cliente corrente, cancellando tutte le informazioni di autenticazione e autorizzazione per tale utente. Elimina tutti i token authN e authZ dal sistema del cliente.

 **Callback attivato:** [setAuthentationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[Torna all&#39;inizio](#top)

</br>

## Definizione callback {#calllback-definitions}

Devi implementare questi callback per gestire le risposte alle chiamate di richiesta asincrone:

- [titolaritàLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## titolaritàLoaded() {#entitlementLoaded}

**Descrizione:** Attivazione quando Access Enabler ha completato l&#39;inizializzazione ed è pronto per ricevere le richieste. Implementa questo callback per sapere quando avviare la comunicazione con l&#39;API di Access Enabler.
</br>

[Torna all&#39;inizio](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**Descrizione:** Implementa questo callback per ricevere le informazioni di configurazione e l&#39;elenco MVPD.

**Parametri:**

- *configXML*: oggetto xml contenente la configurazione per il RICHIEDENTE corrente, incluso l&#39;elenco MVPD.

 
**Attivazione da:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[Torna all&#39;inizio](#top)

</br>

## displayProviderDialog(provider) {#displayproviderdialog(providers)}

**Descrizione:** Implementa questo callback per richiamare la tua interfaccia utente personalizzata per la selezione del provider. Nella finestra di dialogo, utilizza il nome visualizzato (e il logo opzionale) per fornire le scelte del cliente. Quando il cliente ha fatto una scelta e ha chiuso la finestra di dialogo, invia l&#39;ID associato per il provider scelto nella chiamata a *setSelectedProvider()*.

**Parametri:**

- *provider* - Matrice di oggetti che rappresenta gli MVPD richiesti:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**Attivazione da:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[Torna all&#39;inizio](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**Descrizione:** Implementa questo callback se l&#39;utente ha selezionato un MVPD che richiede un iFrame in cui visualizzare la sua interfaccia utente della pagina di accesso di autenticazione.

**Attivazione da:**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [Torna all&#39;inizio](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**Descrizione:** Implementa questo callback per ricevere lo stato di autenticazione (1=autenticato o 0=non autenticato) e un messaggio di errore descrittivo se si è verificato un errore durante il tentativo di determinare lo stato di autenticazione (stringa vuota al completamento del controllo).

>[!NOTE]
> 
>Se utilizzi la corrente, [Segnalazione avanzata degli errori](/help/authentication/error-reporting.md) è possibile ignorare il parametro errorCode inviato a questa funzione.  Tuttavia, i flag isAuthenticated sono ancora in uso per monitorare lo stato di autenticazione di un utente nel flusso di adesione


**Parametri:**

- *isAuthenticated* - Fornisce lo stato di autenticazione: 1 (autenticato) o 0 (non autenticato).
- *errorCode* - Qualsiasi errore che si è verificato durante la determinazione dello stato di autenticazione. Una stringa vuota, se nessuna.

 
**Attivazione da:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[Torna all&#39;inizio](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>Il tipo di dispositivo e il sistema operativo sono derivati dall&#39;utilizzo di una libreria Java pubblica (<http://java.net/projects/user-agent-utils>) e la stringa dell&#39;agente utente. Tieni presente che queste informazioni vengono fornite solo come modo approssimativo per suddividere le metriche operative in categorie di dispositivi, ma che l’Adobe non può assumersi alcuna responsabilità per i risultati errati. Utilizza di conseguenza la nuova funzionalità.

**Descrizione:** Implementa questo callback per ricevere i dati di tracciamento quando si verificano eventi specifici. Puoi utilizzarlo, ad esempio, per tenere traccia di quanti utenti hanno effettuato l’accesso con le stesse credenziali. Il tracciamento non è attualmente configurabile. Con l’autenticazione Adobe Primetime 1.6, `sendTrackingData()` riporta inoltre informazioni sul dispositivo, sul client di Access Enabler e sul tipo di sistema operativo. La `sendTrackingData()` callback rimane compatibile con le versioni precedenti.\
 
- Valori possibili per il tipo di dispositivo:
   - computer
   - tablet
   - mobile
   - sogliola
   - sconosciuto

- Valori possibili per il tipo di client di Access Enabler:
   - html5
   - ios
   - androide


Passa il tipo di evento e una matrice di informazioni associate. I tipi di evento sono:

| mvpdSelection | L&#39;utente ha selezionato un MVPD in una finestra di dialogo di selezione del provider. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | Controllo di autenticazione completato. |
| authorizationDetection | Richiesta di autorizzazione completata. |

</br>
I dati sono specifici per ogni tipo di evento:
</br>

| Tipo evento (String) | Dati (array) |
|:--- | :--- |
| mvpdSelection | 0: MVPD selezionato |
|  | 1: Tipo di dispositivo |
|  | 2: Access Enabler, tipo di client |
|  | 3: OS |
| authenticationDetection | 0: Se la richiesta del token è riuscita (true/false) |
|  | 1: ID MVPD |
|  | 2: GUID |
|  | 3: Token già presente nella cache (true/false) |
|  | 4. Tipo di dispositivo |
|  | 5: Access Enabler, tipo di client |
|  | 6. OS |
| authorizationDetection | 0: Se la richiesta del token è riuscita (true/false) |
|  | 1: ID MVPD |
|  | 2: GUID |
|  | 3: Token già presente nella cache (true/false) |
|  | 4. Errore |
|  | 5: Dettagli |
|  | 6. Tipo di dispositivo |
|  | 7: Access Enabler, tipo di client |
|  | 8: OS |


**Attivazione da:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[Torna all&#39;inizio](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**Descrizione:** Implementa questo callback per ricevere il token per contenuti multimediali di breve durata (inToken) e l’ID della risorsa (inRequestedResourceID) per i quali è stata effettuata una richiesta di autorizzazione o di autorizzazione del controllo ed è stato completato con successo.

**Attivazione da:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[Torna all&#39;inizio](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**Descrizione:** Implementa questo callback da segnalare in caso di errore di un&#39;autorizzazione o di una richiesta di autorizzazione del controllo. Facoltativamente può essere utilizzato da un MVPD per fornire un messaggio personalizzato che deve essere visualizzato dal programmatore.

>[!IMPORTANT]
>
>Questa funzione di callback fa parte del vecchio sistema di segnalazione degli errori di autenticazione Primetime. Viene mantenuto per la compatibilità con le versioni precedenti, ma non è necessario utilizzare questa funzione se sono stati implementati i propri callback utilizzando il sistema di reporting degli errori avanzati corrente. Il sistema di segnalazione degli errori più recente fornisce informazioni più dettagliate sul motivo per cui un&#39;autorizzazione (o un&#39;altra operazione) non è riuscita, insieme a corsi d&#39;azione consigliati per ogni tipo di errore o avviso.

**Parametri:**

- *inRequestedResourceID* - Una stringa che fornisce l&#39;ID risorsa utilizzato nella richiesta di autorizzazione.
- *inRequestErrorCode* - Una stringa che visualizza il codice di errore di autenticazione di Adobe Primetime, indicando il motivo dell&#39;errore; i valori possibili sono &quot;Errore utente non autenticato&quot; e &quot;Errore utente non autorizzato&quot;; per ulteriori dettagli, vedi &quot;Codici di errore di callback&quot; di seguito.
- *inRequestDetailedErrorMessage* - Stringa descrittiva aggiuntiva adatta alla visualizzazione. Se questa stringa descrittiva non è disponibile per alcun motivo, l&#39;autenticazione Adobe Primetime invia una stringa vuota **(&quot;&quot;)**.  Può essere utilizzato da un MVPD per trasmettere messaggi di errore personalizzati o messaggi relativi alle vendite. Ad esempio, se a un abbonato viene negata l&#39;autorizzazione per una risorsa, l&#39;MVPD potrebbe rispondere con un `*inRequestDetailedErrorMessage*` quali: **&quot;Al momento non hai accesso a questo canale nel tuo pacchetto. Per aggiornare il pacchetto, fai clic su \*qui\*.&quot;** Il messaggio viene passato dall&#39;autenticazione Adobe Primetime tramite questo callback al sito del programmatore. Il programmatore ha quindi la possibilità di visualizzarlo o ignorarlo. L’autenticazione Adobe Primetime può anche utilizzare `*inRequestDetailedErrorMessage*` notificare al programmatore la condizione che potrebbe aver causato un errore. Ad esempio: **&quot;Errore di rete durante la comunicazione con il servizio di autorizzazione del provider&quot;.**

 

**Attivazione da:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[Torna all&#39;inizio](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**Descrizione:** Callback attivato da Access Enabler che consegna l&#39;elenco delle risorse autorizzate restituito dopo una chiamata a `checkPreauthorizedResources()`.

**Parametri:**

- *authorizedResources*: elenco delle risorse autorizzate.

**Attivazione da:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[Torna all&#39;inizio](#top)

</br>

## setMetadataStatus(key, encrypted, data) {#setMetadataStatus(key,encrypted,data)}

**Descrizione:** Callback attivato da Access Enabler che distribuisce i metadati richiesti tramite un `getMetadata()` chiama.

**Ulteriori informazioni:** [Metadati utente](#userMetadata)

**Parametri:**

- *key (String)*: Chiave dei metadati per i quali è stata effettuata la richiesta.
- *crittografato (booleano)*: Flag che indica se il &quot;valore&quot; è crittografato o meno. Se questo è &quot;vero&quot;, allora &quot;valore&quot; sarà in realtà una rappresentazione JSON Web Encrypted del valore effettivo. 
- *data (oggetto JSON)*: Un oggetto JSON con la rappresentazione dei metadati.Per richieste semplici (&#39;`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&quot;), risultato è un valore String (che rappresenta l&#39;Authentication TTL, Authorization TTL o Device ID). Nel caso di una richiesta di metadati utente, il risultato può essere un oggetto primitivo o JSON che rappresenta il payload dei metadati. La struttura effettiva degli oggetti metadati utente JSON è simile alla seguente:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```
 

Ad esempio:

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```
 

**Attivazione da:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[Torna all&#39;inizio](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**Descrizione:** Implementa questo callback per ricevere l&#39;MVPD attualmente selezionato e il risultato dell&#39;autenticazione dell&#39;utente corrente racchiuso in `result` parametro . La `result` è un oggetto con le seguenti proprietà:

- **MVPD** MVPD attualmente selezionato o nullo se non è stato selezionato alcun MVPD.
- **AE\_State** Il risultato dell&#39;autenticazione per l&#39;utente corrente, uno tra &quot;Nuovo utente&quot;, &quot;Utente non autenticato&quot; o &quot;Utente autenticato&quot;

 **Attivazione da:** [getSelectedProvider()](#getSelProv)

</br>

[Torna all&#39;inizio](#top)

</br>

### Codici di errore callback {#callback-error-codes}

| Errori generici |  |
|:--- | :--- | 
| Errore interno | Errore di sistema durante il tentativo di elaborare la richiesta. |
| Errore del provider non selezionato | Si verifica quando il cliente annulla nella finestra di dialogo di selezione del provider |
| Errore del provider non disponibile | Si verifica quando non sono disponibili provider. |

| Errori di autenticazione |  |
|:--- | :--- | 
| Errore di autenticazione generico | Restituito quando il motivo non è noto o non può essere pubblicato. |
| Errore di autenticazione interna | Errore di sistema durante il tentativo di autenticazione. |
| Errore utente non autenticato | Utente non autenticato. |
| Errore di più richieste di autenticazione | Sono state ricevute richieste di autenticazione aggiuntive prima del completamento della prima. |

| Errori di autorizzazione |  |
|:--- | :--- | 
| Errore di autorizzazione generico | Restituito quando il motivo non è noto o non può essere pubblicato. |
| Errore di autorizzazione interna | Errore di sistema durante il tentativo di autorizzazione. |
| Errore non autorizzato dell&#39;utente | Il cliente non è autorizzato a visualizzare il contenuto richiesto. |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[Torna all&#39;inizio](#top)

