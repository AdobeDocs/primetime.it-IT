---
title: Riferimento API di iOS/tvOS
description: Riferimento API di iOS/tvOS
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '7065'
ht-degree: 0%

---


# Guida di riferimento dell&#39;API SDK per iOS/tvOS {#iostvos-sdk-api-reference}

- [Introduzione](#intro)
- [Riferimento API](#apis)
- [Tracciamento degli eventi](#tracking)
- [Informazioni correlate](#related)

>[!NOTE]
>
>**Avviso**: Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro}

Questa pagina descrive i metodi e le funzioni di callback esposti dal client nativo iOS/tvOS per l&#39;autenticazione Adobe Primetime. I metodi e le funzioni di callback qui descritti sono definiti nella `AccessEnabler.h` e `EntitlementDelegate.h` file di intestazione; sono disponibili in iOS AccessEnabler SDK qui: `[SDK directory]/AccessEnabler/headers/api/`


Documentazione associata:

- Per una descrizione del flusso di base dell&#39;adesione all&#39;autenticazione Primetime, vedi [Flusso di adesione](https://tve.helpdocsonline.com/entitlement-flow).
- Per informazioni dettagliate su come implementare il flusso di adesione all’autenticazione Primetime utilizzando questa API, consulta la sezione [Guida di riferimento per l’integrazione di iOS](/help/authentication/iostvos-sdk-cookbook.md).
- Per l&#39;SDK più recente di iOS AccessEnabler, visita <https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library>. 

 

**Nota:** L’Adobe ti incoraggia a utilizzare solo l’autenticazione Primetime *pubblico* API:

- Le API pubbliche sono disponibili e testate completamente su tutti i tipi di client supportati. Per qualsiasi funzionalità pubblica, assicuriamo che ogni tipo di client abbia una versione corrispondente dei metodi associati.
- Le API pubbliche devono essere il più stabili possibile, per supportare la compatibilità con le versioni precedenti e garantire che le integrazioni dei partner non vengano interrotte. Tuttavia, per le API non pubbliche, ci riserviamo il diritto di modificare la firma in qualsiasi momento futuro. Se incontri un flusso particolare che non può essere supportato tramite una combinazione delle chiamate API pubbliche di autenticazione Primetime correnti, l&#39;approccio migliore è quello di avvisarci. Tenendo conto delle tue esigenze, possiamo modificare le API pubbliche e fornire una soluzione stabile che prosegua.

</br>

## Riferimento API {#apis}

- [init](#initWithSoftwareStatement):softwareStatement - Crea l&#39;istanza dell&#39;oggetto AccessEnabler.
- **[OBSOLETO]** [init](#init) - Crea un&#39;istanza dell&#39;oggetto AccessEnabler.
- [setOptions:options:](#setOptions) - Configura le opzioni SDK globali come profilo o visitorID.
- [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:serviceProviders:](#setReqV3) - Stabilisce l&#39;identità del programmatore.
- **[OBSOLETO]** [setRequestor:signedRequestorId:](#setReq), [setRequestor:signedRequestorId:serviceProviders:](#setReq) - Stabilisce l&#39;identità del programmatore.
- **[OBSOLETO]** [setRequestor:signedRequestorId:segreto:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos) - Stabilisce l&#39;identità del programmatore.
- [setRequestorComplete:](#setReqComplete) - Comunica all&#39;applicazione che la fase di configurazione è completa.
- [checkAuthentication](#checkAuthN) - Controlla lo stato di autenticazione dell&#39;utente corrente.
- [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN) - Avvia il flusso di lavoro di autenticazione completo.
- [getAuthentication:filter](#getAuthN_filter),[ ](#getAuthN_filter)[getAuthentication:withData:](#getAuthN)[andFilter](#getAuthN_filter) - Avvia il flusso di lavoro di autenticazione completo.
- [displayProviderDialog:](#dispProvDialog) - Informa l&#39;applicazione per creare un&#39;istanza degli elementi dell&#39;interfaccia utente appropriati per consentire all&#39;utente di selezionare un MVPD.
- [setSelectedProvider:](#setSelProv) - informa AccessEnabler della selezione MVPD dell&#39;utente.
- [navigaToUrl:](#nav2url) - Comunica all&#39;applicazione che l&#39;utente deve essere presentato con la pagina di accesso MVPD.
- [navigaToUrl:useSVC:](#nav2urlSVC) - Comunica all&#39;applicazione che l&#39;utente deve essere presentato con la pagina di accesso MVPD, utilizzando SFSafariViewController
- [handleExternalURL:url](#handleExternalURL) - Completa il flusso di autenticazione/logout.
- **[OBSOLETO]** [getAuthenticationToken](#getAuthNToken) - Richiede il token di autenticazione dal server back-end.
- [setAuthenticationStatus:errorCode:](#setAuthNStatus) - informa l&#39;applicazione dello stato del flusso di autenticazione.
- [checkPreauthorizedResources:](#checkPreauth) - Determina se l&#39;utente è già autorizzato a visualizzare risorse protette specifiche.
- [checkPreauthorizedResources:cache:](#checkPreauthCache) - Determina se l&#39;utente è già autorizzato a visualizzare risorse protette specifiche.
- [preauthorizedResources:](#preauthResources) - Fornisce un elenco delle risorse che l&#39;utente è già autorizzato a visualizzare.
- [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ) - Controlla lo stato di autorizzazione dell&#39;utente corrente.
- [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ) - Avvia il flusso di autorizzazione.
- [setToken:forResource:](#setToken) - Comunica all&#39;applicazione che il flusso di autorizzazione è stato completato correttamente.
- [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) - Comunica all&#39;applicazione che il flusso di autorizzazione non è riuscito.
- [disconnessione](#logout) - Avvia il flusso di logout.
- [getSelectedProvider](#getSelProv) - Determina il provider attualmente selezionato.
- [selectedProvider:](#selProv) - Fornisce informazioni sull&#39;MVPD attualmente selezionato alla tua applicazione.
- [getMetadata:](#getMeta) - Recupera le informazioni esposte come metadati dalla libreria AccessEnabler.
- [presentTvProviderDialog:](#presentTvDialog) - Informa l&#39;applicazione per visualizzare la finestra di dialogo SSO Apple.
- [dismissTvProviderDialog:](#dismissTvDialog) - Informa l&#39;applicazione per nascondere la finestra di dialogo SSO di Apple.
- [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus) - Fornisce i metadati richiesti da un [getMetadata:](#getMeta) chiama.
- [sendTrackingData:forEventType:](#sendTracking) - Fornisce informazioni sui dati di tracciamento.
- [MVPD](#mvpd) - La classe MVPD. [Contiene informazioni sull&#39;MVPD]


### init:softwareStatement {#initWithSoftwareStatement}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Crea un&#39;istanza dell&#39;oggetto AccessEnabler. Deve essere presente una singola istanza di AccessEnabler per ogni istanza di applicazione.

| **Chiamata API: Costruttore iOS AccessEnabler** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**Disponibilità:** v3.0+

**Parametri:**

- softwareStatement: Una stringa che identifica l&#39;applicazione nel sistema di Adobe. Controllare come ottenere un&#39;istruzione software.

[Torna all&#39;inizio...](#apis)



### init - [OBSOLETO]{#init}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Crea un&#39;istanza dell&#39;oggetto AccessEnabler. Deve essere presente una singola istanza di AccessEnabler per ogni istanza di applicazione.

| Chiamata API: Costruttore iOS AccessEnabler |
| --- |
| ```- (id) init;``` |

**Disponibilità:** v1.0+ **Fino a:** v3.0

**Parametri:** Nessuno

 

[Torna all&#39;inizio...](#apis)

</br>

### setOptions:options {#setOptions}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Configura le opzioni SDK globali. Accetta un dizionario NSDictionary come argomento. I valori del dizionario verranno passati al server insieme a ogni chiamata di rete effettuata dall&#39;SDK.

**Nota:** I valori verranno passati al server indipendentemente dal flusso corrente (autenticazione/autorizzazione). Se si desidera modificare i valori, è possibile chiamare questo metodo in qualsiasi momento.

| Chiamata API: setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**Disponibilità:** v2.3.0+

**Parametri:**

- *options*: Un dizionario NSDictionary contenente opzioni SDK globali. Al momento sono disponibili le seguenti opzioni:
   - **applicationProfile** - Può essere utilizzato per effettuare configurazioni server basate su questo valore.
   - **visitorID** - Il Marketing Cloud visitorID. Questo valore può essere successivamente utilizzato per i rapporti di analisi avanzati.
   - **handleSVC** - Valore booleano che indica se il programmatore gestirà SFSafariViewControllers. Vedi [Supporto SFSafariViewController in iOS SDK 3.2+](https://tve.helpdocsonline.com/sfsafariviewcontroller-support-on-ios-sdk-3.2) per ulteriori dettagli.
      - Se impostato su **false,** l&#39;SDK presenta automaticamente all&#39;utente finale un SFSafariViewController. L’SDK proseguirà la navigazione all’URL della pagina di accesso MVPD.
      - Se impostato su **vero,** l&#39;SDK **NOT** presenta automaticamente all&#39;utente finale un SFSafariViewController. L’SDK verrà attivato ulteriormente **naviga(toUrl:{url}, useSVC:YES)**.
- **device\_info** - Informazioni sul cliente come descritto qui:
   <https://tve.helpdocsonline.com/passing-client-information>.

 

[Torna all&#39;inizio...](#apis)


### setRequestor:requestorID, setRequestor:requestorID:serviceProviders: {#setReqV3}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Stabilisce l&#39;identità del programmatore. A ciascun programmatore viene assegnato un ID univoco al momento della registrazione con Adobe per il sistema di autenticazione Primetime. Quando si tratta di token SSO e remoti, lo stato di autenticazione può cambiare quando l&#39;applicazione è in background, setRequestor può essere richiamato nuovamente quando l&#39;applicazione viene portata in primo piano per sincronizzarsi con lo stato del sistema (recupera un token remoto se SSO è abilitato o elimina il token locale se nel frattempo si verifica un logout).


La risposta del server contiene un elenco di MVPD insieme ad alcune informazioni di configurazione collegate all&#39;identità del programmatore. La risposta del server viene utilizzata internamente dal codice AccessEnabler . Solo lo stato dell&#39;operazione (ovvero SUCCESS/FAIL) viene presentato all&#39;applicazione tramite il `setRequestorComplete:` callback.

Se la `urls` Il parametro non viene utilizzato, la chiamata di rete risultante esegue il targeting dell&#39;URL predefinito del provider di servizi: l’ambiente RELEASE/produzione di Adobe.


Se viene fornito un valore per `urls` , la chiamata di rete risultante esegue il targeting di tutti gli URL forniti nel `urls` parametro . Tutte le richieste di configurazione vengono attivate simultaneamente in thread separati. Il primo risponditore ha la precedenza quando si compila l&#39;elenco degli MVPD. Per ogni MVPD nell&#39;elenco, AccessEnabler ricorda l&#39;URL del provider di servizi associato. Tutte le richieste di adesione successive vengono indirizzate all&#39;URL associato al provider di servizi che è stato abbinato all&#39;MVPD di destinazione durante la fase di configurazione.

| Chiamata API: configurazione richiedente |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**Disponibilità:** v3.0+

| Chiamata API: configurazione richiedente |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**Disponibilità:** v3.0+

**Parametri:**

- *requestorID*: ID univoco associato al programmatore. Passa l&#39;ID univoco assegnato da Adobe al tuo sito la prima volta che ti registri con il servizio di autenticazione Primetime.
- *url*: Parametro facoltativo; per impostazione predefinita, viene utilizzato il provider di servizi Adobe (http://sp.auth.adobe.com/). Questo array consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). È possibile utilizzarlo per specificare più istanze del provider di servizi di autenticazione Primetime. In questo modo, l&#39;elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al fornitore di servizi più veloce; cioè, il fornitore che ha risposto per primo e che supporta quel MVPD.

   **Nota:** Se chiamato senza `serviceProviders` , la libreria recupererà la configurazione dal provider di servizi predefinito (ovvero, `https://sp.auth.adobe.com` per il profilo di produzione o https://sp.auth-staging.adobe.com per il profilo di staging). Se la `serviceProviders` viene fornito, deve essere un array di URL. Le informazioni di configurazione vengono recuperate da tutti gli endpoint specificati e vengono unite. Se nelle risposte dei fornitori di servizi sono presenti informazioni duplicate, il conflitto viene risolto a favore del server che risponde più velocemente (ad esempio, il server con il tempo di risposta più breve ha la precedenza).

 

**Callback attivato:** [`setRequestorComplete:`](#setReqComplete)

 

[Torna all&#39;inizio...](#apis)

</br>

### setRequestor:setSignedRequestorId:setRequestor:setSignedRequestorId:serviceProviders: - [OBSOLETO] {#setReq}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Stabilisce l&#39;identità del programmatore. A ciascun programmatore viene assegnato un ID univoco al momento della registrazione con Adobe per il sistema di autenticazione Primetime. Quando si tratta di token SSO e remoti, lo stato di autenticazione può cambiare quando l&#39;applicazione è in background, setRequestor può essere richiamato nuovamente quando l&#39;applicazione viene portata in primo piano per sincronizzarsi con lo stato del sistema (recupera un token remoto se SSO è abilitato o elimina il token locale se nel frattempo si è verificato un logout).

La risposta del server contiene un elenco di MVPD insieme ad alcune informazioni di configurazione collegate all&#39;identità del programmatore. La risposta del server viene utilizzata internamente dal codice AccessEnabler . Solo lo stato dell&#39;operazione (ovvero SUCCESS/FAIL) viene presentato all&#39;applicazione tramite il `setRequestorComplete:` callback.

Se la `urls` Il parametro non viene utilizzato, la chiamata di rete risultante esegue il targeting dell&#39;URL predefinito del provider di servizi: l’ambiente RELEASE/produzione di Adobe.

Se viene fornito un valore per `urls` , la chiamata di rete risultante esegue il targeting di tutti gli URL forniti nel `urls` parametro . Tutte le richieste di configurazione vengono attivate simultaneamente in thread separati. Il primo risponditore ha la precedenza quando si compila l&#39;elenco degli MVPD. Per ogni MVPD nell&#39;elenco, AccessEnabler ricorda l&#39;URL del provider di servizi associato. Tutte le richieste di adesione successive vengono indirizzate all&#39;URL associato al provider di servizi che è stato abbinato all&#39;MVPD di destinazione durante la fase di configurazione.

| Chiamata API: configurazione richiedente |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**Disponibilità:** v1.0+ **Fino a:** v3.0

| Chiamata API: configurazione richiedente |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**Disponibilità:** v1.0+ **Fino a:** v3.0

**Parametri:**

- *requestorID*: ID univoco associato al programmatore. Passa l&#39;ID univoco assegnato da Adobe al tuo sito la prima volta che ti sei registrato con il servizio di autenticazione Primetime.
- *signedRequestorID*: **Questo parametro esiste in iOS AccessEnabler versione 1.2 e successive.** Una copia del requestor ID con firma digitale con la tua chiave privata. Per ulteriori dettagli, consulta [Registrazione dei client nativi](https://tve.helpdocsonline.com/registering-native-clients).
- *url*: Parametro facoltativo; per impostazione predefinita, viene utilizzato il provider di servizi Adobe (http://sp.auth.adobe.com/). Questo array consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). È possibile utilizzarlo per specificare più istanze del provider di servizi di autenticazione Primetime. In questo modo, l&#39;elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al fornitore di servizi più veloce; cioè, il fornitore che ha risposto per primo e che supporta quel MVPD.

**Note:** Se chiamato senza `serviceProviders` , la libreria recupererà la configurazione dal provider di servizi predefinito (ovvero: `https://sp.auth.adobe.com` per il profilo di produzione o `https://sp.auth-staging.adobe.com` per il profilo di staging). Se la `serviceProviders` viene fornito, deve essere un array di URL. Le informazioni di configurazione vengono recuperate da tutti gli endpoint specificati e vengono unite. Se nelle risposte dei fornitori di servizi sono presenti informazioni duplicate, il conflitto viene risolto a favore del server che risponde più velocemente (ad esempio, il server con il tempo di risposta più breve ha la precedenza).

**Callback attivato:** [`setRequestorComplete:`](#setReqComplete)


[Torna all&#39;inizio...](#apis)

### setRequestor:setSignedRequestorId:segreto:publicKey, setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [OBSOLETO] {#setReq_tvos}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Stabilisce l&#39;identità del programmatore. A ciascun programmatore viene assegnato un ID univoco al momento della registrazione con Adobe per il sistema di autenticazione Primetime. Questa impostazione deve essere eseguita una sola volta durante il ciclo di vita dell&#39;applicazione.

La risposta del server contiene un elenco di MVPD insieme ad alcune informazioni di configurazione collegate all&#39;identità del programmatore. La risposta del server viene utilizzata internamente dal codice AccessEnabler . Solo lo stato dell&#39;operazione (ovvero SUCCESS/FAIL) viene presentato all&#39;applicazione tramite il `setRequestorComplete:` callback.

Se la `urls` Il parametro non viene utilizzato, la chiamata di rete risultante esegue il targeting dell&#39;URL predefinito del provider di servizi: l’ambiente RELEASE/produzione di Adobe.

Se viene fornito un valore per `urls` , la chiamata di rete risultante esegue il targeting di tutti gli URL forniti nel `urls` parametro . Tutte le richieste di configurazione vengono attivate simultaneamente in thread separati. Il primo risponditore ha la precedenza quando si compila l&#39;elenco degli MVPD. Per ogni MVPD nell&#39;elenco, AccessEnabler ricorda l&#39;URL del provider di servizi associato. Tutte le richieste di adesione successive vengono indirizzate all&#39;URL associato al provider di servizi che è stato abbinato all&#39;MVPD di destinazione durante la fase di configurazione.



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: configurazione richiedente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilità:** v2.0+ **Fino a:** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: configurazione richiedente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**Disponibilità:** v2.0+ **Fino a:** v3.0

**Parametri:**

- *requestorID*: ID univoco associato al programmatore. Passa l&#39;ID univoco assegnato da Adobe al tuo sito la prima volta che ti sei registrato con il servizio di autenticazione Primetime.
- *signedRequestorID*: **Questo parametro esiste in iOS AccessEnabler versione 1.2 e successive.** Una copia del requestor ID con firma digitale con la tua chiave privata. Per ulteriori dettagli, consulta [Registrazione dei client nativi](https://tve.helpdocsonline.com/registering-native-clients).
- *url*: Parametro facoltativo; per impostazione predefinita, viene utilizzato il provider di servizi Adobe (http://sp.auth.adobe.com/). Questo array consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). È possibile utilizzarlo per specificare più istanze del provider di servizi di autenticazione Primetime. In questo modo, l&#39;elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al fornitore di servizi più veloce; cioè, il fornitore che ha risposto per primo e che supporta quel MVPD.
- secret e publicKey: Chiave segreta e pubblica utilizzata per firmare le chiamate della seconda schermata. Per ulteriori informazioni, consulta la sezione [Documentazione senza client](#create_dev).

Se chiamato senza `serviceProviders` , la libreria recupererà la configurazione dal provider di servizi predefinito (ovvero, `https://sp.auth.adobe.com` per il profilo di produzione o https://sp.auth-staging.adobe.com per il profilo di staging). Se la `serviceProviders` viene fornito, deve essere un array di URL. Le informazioni di configurazione vengono recuperate da tutti gli endpoint specificati e vengono unite. Se nelle risposte dei fornitori di servizi sono presenti informazioni duplicate, il conflitto viene risolto a favore del server che risponde più velocemente (ad esempio, il server con il tempo di risposta più breve ha la precedenza).

**Callback attivato:** [`setRequestorComplete:`](#setReqComplete)

[Torna all&#39;inizio...](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler che informa l&#39;applicazione del completamento della fase di configurazione. Questo è un segnale che l’app può iniziare a emettere richieste di adesione. L&#39;applicazione non può emettere richieste di adesione fino al completamento della fase di configurazione.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: configurazione del richiedente completata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilità:** v1.0+

**Parametri**:

- *status*: può assumere uno dei seguenti valori:
   - `ACCESS_ENABLER_STATUS_SUCCESS` - fase di configurazione completata
   - `ACCESS_ENABLER_STATUS_ERROR` - fase di configurazione non riuscita

**Attivazione da:**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[Torna all&#39;inizio...](#apis)

</br>

### checkAuthentication {#checkAuthN}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Controlla lo stato di autenticazione dell&#39;utente corrente.
A tale scopo, cerca un token di autenticazione valido nello spazio di archiviazione locale dei token. La chiamata di questo metodo non esegue chiamate di rete. Viene utilizzato dall’applicazione per eseguire una query sullo stato di autenticazione dell’utente e aggiornare di conseguenza l’interfaccia utente (ad esempio, per aggiornare l’interfaccia utente di accesso/disconnessione). Lo stato di autenticazione viene comunicato all’applicazione tramite il [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) callback.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: verifica stato autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[Torna all&#39;inizio...](#apis)

</br>

### getAuthentication, getAuthentication:withData: {#getAuthN}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Avvia il flusso di lavoro di autenticazione completo. Inizia controllando lo stato di autenticazione. Se non è già autenticato, viene avviato il computer dello stato del flusso di autenticazione:

- se l&#39;ultimo tentativo di autenticazione è riuscito, la fase di selezione MVPD viene ignorata e la [`navigateToUrl:`](#nav2url) viene attivato il callback. L&#39;applicazione utilizza questo callback per creare un&#39;istanza del controllo WebView che presenta l&#39;utente alla pagina di accesso dell&#39;MVPD. **[NOTA: A partire da Access Enabler 1.5, questa funzionalità non è disponibile a causa di una limitazione nell&#39;SDK].**
- se l&#39;ultimo tentativo di autenticazione non ha avuto esito positivo o se l&#39;utente si è disconnesso in modo esplicito, l&#39; [`displayProviderDialog:`](#dispProvDialog) viene attivato il callback. L&#39;applicazione utilizza questo callback per visualizzare l&#39;interfaccia utente di selezione MVPD. È inoltre necessario che l&#39;app riprenda il flusso di autenticazione informando la libreria AccessEnabler sulla selezione MVPD dell&#39;utente tramite la [`setSelectedProvider:`](#setSelProv) metodo .

Poiché le credenziali dell&#39;utente sono verificate nella pagina di accesso MVPD, l&#39;applicazione è necessaria per monitorare le operazioni di reindirizzamento multiple che si verificano mentre l&#39;utente si autentica nella pagina di accesso dell&#39;MVPD. Quando si immettono le credenziali corrette, il controllo WebView viene reindirizzato a un URL personalizzato definito dalla `ADOBEPASS_REDIRECT_URL` costante. Questo URL non deve essere caricato da WebView. L&#39;applicazione deve intercettare questo URL e interpretare questo evento come un segnale del completamento della fase di accesso. Deve quindi trasferire il controllo ad AccessEnabler per completare il flusso di autenticazione (chiamando il [handleExternalURL](#handleExternalURL) metodo).

Infine, lo stato di autenticazione viene comunicato all&#39;applicazione tramite il [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Disponibilità:** v1.9+

**Parametri:**

- *forceAuthn*: Flag che specifica se il flusso di autenticazione deve essere avviato, indipendentemente dal fatto che l&#39;utente sia già autenticato o meno.
- *dati*: Un dizionario costituito da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK. 

**Callback attivato:** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[Torna all&#39;inizio...](#apis)

</br>

### getAuthentication:filter, getAuthentication:withData:andFilter {#getAuthN_filter}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Avvia il flusso di lavoro di autenticazione completo. Inizia controllando lo stato di autenticazione. Se non è già autenticato, viene avviato il computer dello stato del flusso di autenticazione:

- [presentTvProviderDialog()](#presentTvDialog) verrà chiamato se il richiedente corrente ha almeno un MVPD che supporta SSO. Se nessun MVPD supporta SSO, il flusso di autenticazione classico verrà avviato e il parametro del filtro verrà ignorato.
- Dopo che l&#39;utente completa il flusso SSO di Apple [dismissTvProviderDialog()](#dismissTvDialog) verrà attivato e il processo di autenticazione verrà completato.\
    

Infine, lo stato di autenticazione viene comunicato all&#39;applicazione tramite il [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback.

**Disponibilità:** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parametri:**

- *forceAuthn*: Flag che specifica se il flusso di autenticazione deve essere avviato, indipendentemente dal fatto che l&#39;utente sia già autenticato o meno.
- *dati*: Un dizionario costituito da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK. 
- filtro: Un dizionario con due elenchi di ID MVPD che dovrebbero essere visualizzati nella finestra di dialogo SSO di Apple. Qualsiasi MVPD che non supporta SSO verrà ignorato, ma l&#39;ordine verrà rispettato. Il dizionario deve avere due chiavi:
   - TV\_PROVIDERS: Un elenco con tutti gli MVPD che dovrebbero essere visualizzati nel selettore
   - FEATURED\_TV\_PROVIDERS: Un elenco con tutti gli MVPD che devono essere contrassegnati come descritto nel selettore. Anche gli MVPD presenti in questo elenco devono essere specificati nell&#39;elenco TV\_PROVIDERS.

**Disponibilità:** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**Parametri:**

- *forceAuthn*: Flag che specifica se il flusso di autenticazione deve essere avviato, indipendentemente dal fatto che l&#39;utente sia già autenticato o meno.
- *dati*: Un dizionario costituito da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK. 
- filtro: Elenco degli ID MVPD che devono essere visualizzati nella finestra di dialogo SSO di Apple. Qualsiasi MVPD che non supporta SSO verrà ignorato, ma l&#39;ordine verrà rispettato.

**Callback attivato:** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[Torna all&#39;inizio...](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler per informare l&#39;applicazione che è necessario creare un&#39;istanza degli elementi dell&#39;interfaccia utente appropriati per consentire all&#39;utente di selezionare l&#39;MVPD desiderato. Il callback fornisce un elenco di oggetti MVPD con informazioni aggiuntive che possono aiutare a creare correttamente il pannello dell’interfaccia utente di selezione (come l’URL che punta al logo dell’MVPD, il nome visualizzato descrittivo, ecc.)

Una volta che l&#39;utente ha selezionato il MVPD desiderato, l&#39;applicazione di livello superiore è necessaria per riprendere il flusso di autenticazione chiamando `setSelectedProvider:` e trasmettendolo l&#39;ID dell&#39;MVPD corrispondente alla selezione dell&#39;utente.

**Interruzione del flusso di autenticazione** - Questo è un punto in cui l&#39;utente può premere il pulsante &quot;Indietro&quot;, che equivale ad interrompere il flusso di autenticazione. In questo caso, l&#39;applicazione deve chiamare il [setSelectedProvider:](#setSelProv) , passando null come parametro, per dare ad AccessEnabler l&#39;opportunità di reimpostare il proprio computer dello stato di autenticazione.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: visualizzare l'interfaccia utente di selezione MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**Disponibilità:** v1.0+

**Parametri**:

- *mvpds*: elenco di oggetti MVPD contenenti informazioni relative a MVPD che l&#39;applicazione può utilizzare per creare gli elementi dell&#39;interfaccia utente di selezione MVPD.

**Attivazione da:** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[Torna all&#39;inizio...](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene chiamato dall&#39;applicazione per informare Access Enabler della selezione MVPD dell&#39;utente. L&#39;applicazione può utilizzare questo metodo per selezionare o modificare il provider di servizi utilizzato per l&#39;autenticazione.

Se l&#39;MVPD selezionato è un MVPD TempPass, si autenticherà automaticamente con quell&#39;MVPD senza dover chiamare getAuthentication() in seguito.

Tieni presente che questo non è possibile per il Passaggio temporaneo promozionale in cui vengono forniti parametri aggiuntivi sul metodo getAuthentication() .

Al passaggio *null* come parametro, Access Enabler presuppone che l&#39;utente abbia annullato il flusso di autenticazione (cioè ha premuto il pulsante &quot;Indietro&quot;) e risponde reimpostando la macchina dello stato di autenticazione e chiamando il [setAuthenticationStatus:errorCode:](#setAuthNStatus) callback con `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` codice di errore.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: imposta il provider attualmente selezionato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[Torna all&#39;inizio...](#apis)

</br>

#### navigaToUrl: {#nav2url}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione:** Callback attivato da AccessEnabler per richiedere all&#39;applicazione di creare un&#39;istanza di un controller UIWebView/WKWebView e per caricare l&#39;URL fornito nel callback di **`url`** parametro . Il callback passa il **`url`** che rappresenta l&#39;URL dell&#39;endpoint di autenticazione o l&#39;URL dell&#39;endpoint di logout.

Come UIWebView/WKWebView` `il controller passa attraverso diversi reindirizzamenti, l&#39;applicazione deve monitorare l&#39;attività del controller e rilevare il momento in cui carica un URL personalizzato specifico definito dalla `ADOBEPASS_REDIRECT_URL `costante (ovvero `adobepass://ios.app`). Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che l&#39;autenticazione o il flusso di logout è stato completato e che è sicuro chiudere il controller. Quando il controller carica questo URL personalizzato specifico, l&#39;applicazione deve chiudere UIWebView/WKWebView e chiamare AccessEnabler `handleExternalURL:url `Metodo API.

**Nota:** Si prega di notare che in caso di flusso di autenticazione questo è un punto in cui l&#39;utente ha la capacità di premere il pulsante &quot;Indietro&quot;, che è equivalente all&#39;interruzione del flusso di autenticazione. In questo caso, l&#39;applicazione deve chiamare il [setSelectedProvider:](#setSelProv) passaggio del metodo **`nil`** come parametro e dando la possibilità ad AccessEnabler di reimpostare il proprio computer dello stato di autenticazione.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: visualizzare la pagina di accesso MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri**:

- *url*: l&#39;URL che punta alla pagina di accesso dell&#39;MVPD

**Attivazione da:** [setSelectedProvider:](#setSelProv)

 

[Torna all&#39;inizio...](#apis)

</br>

#### navigaToUrl:useSVC: {#nav2urlSVC}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione:** Callback attivato da AccessEnabler invece del `navigateToUrl:` callback nel caso in cui l&#39;applicazione abbia precedentemente abilitato la gestione manuale di Safari View Controller (SVC) tramite [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) e solo nel caso di MVPD che richiedono Safari View Controller (SVC). Per tutti gli altri MVPDs `navigateToUrl:` verrà chiamato il callback. Vedi[Supporto SFSafariViewController in iOS SDK 3.2+](https://tve.helpdocsonline.com/sfsafariviewcontroller-support-on-ios-sdk-3.2) per informazioni dettagliate su come Safari View Controller (SVC) deve essere gestito.

Simile al `navigateToUrl:` callback del `navigateToUrl:useSVC:` viene attivato da AccessEnabler per richiedere all&#39;applicazione di creare un&#39;istanza di `SFSafariViewController` e per caricare l&#39;URL fornito nel callback **`url`** parametro . Il callback passa il **`url`** che rappresenta l&#39;URL dell&#39;endpoint di autenticazione o l&#39;URL dell&#39;endpoint di logout e **`useSVC`** specifica che l&#39;applicazione deve utilizzare un `SFSafariViewController`.

Come `SFSafariViewController` il controller passa attraverso diversi reindirizzamenti, l&#39;applicazione deve monitorare l&#39;attività del controller e rilevare il momento in cui carica un URL personalizzato specifico definito dal tuo `application's custom scheme` (ad esempio** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`). Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che l&#39;autenticazione o il flusso di logout è stato completato e che è sicuro chiudere il controller. Quando il controller carica questo URL personalizzato specifico, l&#39;applicazione deve chiudere la `SFSafariViewController` e chiama AccessEnabler `handleExternalURL:url `Metodo API.

**Nota:** Si prega di notare che in caso di flusso di autenticazione questo è un punto in cui l&#39;utente ha la capacità di premere il pulsante &quot;Indietro&quot;, che è equivalente all&#39;interruzione del flusso di autenticazione. In questo caso, l&#39;applicazione deve chiamare il [setSelectedProvider:](#setSelProv) passaggio del metodo **`nil`** come parametro e dando la possibilità ad AccessEnabler di reimpostare il proprio computer dello stato di autenticazione.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: visualizza la pagina di accesso MVPD in SFSafariViewController</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:**v 3.2+

**Parametri**:

- *url:* l&#39;URL che punta alla pagina di accesso dell&#39;MVPD
- *useSVC:* se l&#39;url deve essere caricato in SFSafariViewController.

**Attivato da: **[setOptions:](#setOptions) prima [setSelectedProvider:](#setSelProv) 

[Torna all&#39;inizio...](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene chiamato dall&#39;applicazione per completare il flusso di autenticazione o logout. Questo metodo deve essere chiamato subito dopo che l&#39;applicazione rileva il momento in cui il `UIWebView/WKWebView or SFSafariViewController` viene reindirizzato a un URL personalizzato specifico. Nel caso in cui l&#39;applicazione debba utilizzare un `SFSafariViewController `controlla l’URL personalizzato specifico definito dalla `application's custom scheme` (ad esempio`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), altrimenti questo URL personalizzato specifico viene definito dalla `ADOBEPASS_REDIRECT_URL `costante (ovvero `adobepass://ios.app`).

Nel caso del flusso di autenticazione, AccessEnabler completa il flusso recuperando il token di autenticazione dal server back-end e memorizzandolo localmente nell&#39;archivio dei token. AccessEnabler informa l&#39;applicazione che il flusso di autenticazione è completo chiamando il [`setAuthenticationStatus()`](http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus) callback con codice di stato 1 che indica il successo. Se si verifica un errore durante l&#39;esecuzione di questi passaggi, il [`setAuthenticationStatus()`](http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus) il callback viene attivato con un codice di stato pari a 0 che indica un errore di autenticazione e un codice di errore corrispondente.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: completare il flusso di autenticazione o logout</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v3.0+

**Parametri:** 

- *url*: L&#39;URL intercettato dalla ` UIWebView/WKWebView or SFSafariViewController ` come stringa.


**Callback attivato:** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[Torna all&#39;inizio...](#apis)

</br>

#### getAuthenticationToken - [OBSOLETO] {#getAuthNToken}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Completa il flusso di autenticazione richiedendo il token di autenticazione dal server back-end. Questo metodo deve essere chiamato dall&#39;applicazione solo in risposta all&#39;evento in cui il controllo WebView che ospita la pagina di accesso MVPD viene reindirizzato all&#39;URL personalizzato definito dalla `ADOBEPASS_REDIRECT_URL` costante.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: recuperare il token di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+ **Fino a:** v3.0

**Parametri:** Nessuno

**Callback attivato:** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[Torna all&#39;inizio...](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler che informa l&#39;applicazione dello stato del flusso di autenticazione. Ci sono molti luoghi in cui questo flusso può fallire, sia a causa dell&#39;interazione dell&#39;utente o a causa di altri scenari imprevisti (ad esempio, problemi di connettività di rete, ecc.). Questo callback informa l&#39;applicazione dello stato di successo/errore del flusso di autenticazione, fornendo anche informazioni aggiuntive sul motivo dell&#39;errore, se necessario.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: segnalare lo stato del flusso di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**Disponibilità:** v1.0+

**Parametri**:

- *status*: può assumere uno dei seguenti valori:
   - `ACCESS_ENABLER_STATUS_SUCCESS` - flusso di autenticazione completato
   - `ACCESS_ENABLER_STATUS_ERROR` - flusso di autenticazione non riuscito
- *codice*: motivo dell&#39;errore. Se *status* è `ACCESS_ENABLER_STATUS_SUCCESS`, quindi *codice* è una stringa vuota (ad esempio, definita dalla `USER_AUTHENTICATED` costante). In caso di errore, questo parametro può assumere uno dei seguenti valori:
   - `USER_NOT_AUTHENTICATED_ERROR` - Utente non autenticato. In risposta al [checkAuthentication:](#checkAuthN) chiamata del metodo quando non è presente un token di autenticazione valido nella cache del token locale.
   - `PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler ha reimpostato la macchina dello stato di autenticazione dopo il passaggio dell&#39;applicazione di livello superiore *null* a [`setSelectedProvider:`](#setSelProv) per interrompere il flusso di autenticazione.  Presumibilmente l&#39;utente ha annullato il flusso di autenticazione (cioè ha premuto il pulsante &quot;Indietro&quot;).
   - `GENERIC_AUTHENTICATION_ERROR` - Il flusso di autenticazione non è riuscito a causa di motivi quali l&#39;indisponibilità della rete o l&#39;utente ha annullato esplicitamente il flusso di autenticazione.

**Attivazione da:** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[Torna all&#39;inizio...](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per determinare se l&#39;utente è già autorizzato a visualizzare risorse protette specifiche. Lo scopo principale di questo metodo è quello di recuperare informazioni da utilizzare per decorare l’interfaccia utente **(ad esempio, per indicare lo stato di accesso con le icone di blocco e sblocco).**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: imposta il provider attualmente selezionato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.3+

**Parametri:**

- *risorse:* array di risorse per le quali deve essere controllata l’autorizzazione. Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa nella chiamata , ovvero deve essere un valore concordato tra il programmatore e l’MVPD o un frammento RSS multimediale.

**Callback attivato:** [`preauthorizedResources:`](#preauthResources)

[Torna all&#39;inizio...](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per determinare se l&#39;utente è già autorizzato a visualizzare risorse protette specifiche. Lo scopo principale di questo metodo è quello di recuperare informazioni da utilizzare per decorare l’interfaccia utente (ad esempio, per indicare lo stato di accesso con le icone di blocco e sblocco). La **cache** controlla se la cache interna viene utilizzata per la risoluzione delle risorse.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: imposta il provider attualmente selezionato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilità:** v3.1+

 

**Parametri:**

- *risorse:* array di risorse per le quali deve essere controllata l’autorizzazione. Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa nel `getAuthorization:` chiamare, cioè, dovrebbe essere un valore concordato stabilito tra il programmatore e il MVPD o un frammento RSS media.
- *cache:* Valore booleano che specifica se utilizzare la cache interna per la risoluzione delle risorse. Se false, la cache verrà bypassata, dando luogo a chiamate al server ogni volta che questa API viene chiamata.

**Callback attivato:** [`preauthorizedResources:`](#preauthResources)

[Torna all&#39;inizio...](#apis)

</br>

### preauthorizedResources: {#preauthResources}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione:** Callback attivato da `checkPreauthorizedResources:`. Fornisce un elenco delle risorse che l&#39;utente è già autorizzato a visualizzare.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: imposta il provider attualmente selezionato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.3+

**Parametri:**

- *`resources`: array di risorse per le quali l’utente è già autorizzato a visualizzare.

**Attivazione da:** [`checkPreauthorizedResources:`](#checkPreauth)

 

[Torna all&#39;inizio...](#apis)

</br>

### checkAuthorization:, checkAuthorization:withData: {#checkAuthZ}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per controllare lo stato dell&#39;autorizzazione. Inizia controllando prima lo stato di autenticazione. Se non autenticato, il [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) viene attivato il callback e il metodo esce. Se l&#39;utente è autenticato, attiva anche il flusso di autorizzazione. Vedi i dettagli [`getAuthorization:`](#getAuthZ) metodo .


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: verifica lo stato dell'autorizzazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: verifica lo stato dell'autorizzazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.9+

**Parametri:**

- *risorsa*: l’ID della risorsa per la quale l’utente richiede l’autorizzazione.
- *dati*: Un dizionario costituito da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK. 

**Callback attivato:**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[Torna all&#39;inizio...](#apis)

</br>

### getAuthorization:, getAuthorization:withData: {#getAuthZ}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per avviare il flusso di autorizzazione. Se l’utente non è già autenticato, avvia anche il flusso di autenticazione. Se l&#39;utente viene autenticato, AccessEnabler continua a emettere richieste per il token di autorizzazione (se non è presente alcun token di autorizzazione valido nella cache dei token locali) e per il token multimediale di breve durata. Una volta ottenuto il token multimediale breve, il flusso di autorizzazione viene considerato completo. La [setToken:forResource:](#setToken) il callback viene attivato e il token multimediale breve viene consegnato come parametro all&#39;applicazione. Se per qualsiasi motivo l&#39;autorizzazione non riesce, il [tokenRequestFailed:forEventType:](#tokenReqFailed) viene attivato il callback e vengono forniti il codice/i dettagli dell’errore.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autorizzazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di autorizzazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilità:** v1.9+

**Parametri:**

- *risorsa*: l’ID della risorsa per la quale l’utente richiede l’autorizzazione.
- *dati*: Un dizionario costituito da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK. 

**Callback attivato:** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**callback aggiuntivi attivati:**\
Questo metodo può anche attivare i seguenti callback (se viene avviato anche il flusso di autenticazione): `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`\
 
**NOTA: Utilizzare checkAuthorization: / checkAuthorization:withData: invece di getAuthorization: / getAuthorization:withData: quando possibile. getAuthorization: / getAuthorization:withData: Il metodo avvierà un flusso di autenticazione completo (se l&#39;utente non è autenticato) che potrebbe comportare un&#39;implementazione complicata da parte del programmatore.**

[Torna all&#39;inizio...](#apis)

</br>

### setToken:forResource: {#setToken}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler che informa l&#39;applicazione che il flusso di autorizzazione è stato completato correttamente. Anche il token multimediale di breve durata viene consegnato come parametro.\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: flusso di autorizzazione completato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri**:

- *token*: token multimediale di breve durata
- *risorsa*: la risorsa per la quale è stata ottenuta l&#39;autorizzazione

**Attivazione da:** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[Torna all&#39;inizio...](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler che informa l&#39;applicazione di livello superiore che il flusso di autorizzazione non è riuscito.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: flusso di autorizzazione non riuscito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri**:

- *risorsa*: Risorsa per la quale è stata ottenuta l&#39;autorizzazione.
- *codice*: Codice di errore associato allo scenario di errore. Valori possibili:
   - `USER_NOT_AUTHORIZED_ERROR` - impossibile autorizzare l&#39;utente per la risorsa specificata
- *descrizione*: Ulteriori dettagli sullo scenario di errore. Se questa stringa descrittiva non è disponibile per alcun motivo, l&#39;autenticazione Primetime invia una stringa vuota **(&quot;&quot;)**. \
   Questa stringa può essere utilizzata da un MVPD per trasmettere messaggi di errore personalizzati o messaggi relativi alle vendite. Ad esempio, se a un utente iscritto viene negata l&#39;autorizzazione per una risorsa, l&#39;MVPD potrebbe inviare un messaggio come: &quot;Al momento non hai accesso a questo canale nel tuo pacchetto. Per aggiornare il pacchetto, fai clic su **qui**.&quot; Il messaggio viene passato dall&#39;autenticazione Primetime tramite questo callback al programmatore, che ha l&#39;opzione di visualizzarlo o ignorarlo. L’autenticazione di Primetime può inoltre utilizzare questo parametro per fornire la notifica della condizione che potrebbe aver generato un errore. Ad esempio, &quot;Errore di rete durante la comunicazione con il servizio di autorizzazione del provider&quot;.

**Attivazione da:** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[Torna all&#39;inizio...](#apis)

</br>

### disconnessione {#logout}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Questo metodo viene chiamato dall&#39;applicazione per avviare il flusso di logout. La disconnessione è il risultato di una serie di operazioni di reindirizzamento HTTP a causa del fatto che l&#39;utente deve essere disconnesso sia dai server di autenticazione Primetime che dai server MVPD. Poiché questo flusso non può essere completato con una semplice richiesta HTTP inviata dalla libreria AccessEnabler, un `UIWebView/WKWebView or SFSafariViewController` è necessario creare un&#39;istanza del controller per poter seguire le operazioni di reindirizzamento HTTP.

Il flusso di logout è diverso dal flusso di autenticazione in quanto l’utente non è tenuto a interagire con il `UIWebView/WKWebView or SFSafariViewController`  in qualsiasi modo. Pertanto, Adobe consiglia di rendere il controllo invisibile (cioè nascosto) durante il processo di logout.

Viene utilizzato un pattern simile al flusso di autenticazione. iOS AccessEnabler attiva il `navigateToUrl:` callback o `navigateToUrl:useSVC:` per creare un `UIWebView/WKWebView or SFSafariViewController` e per caricare l&#39;URL fornito nel callback `url` parametro . Si tratta dell’URL dell’endpoint di logout sul server back-end. Per tvOS AccessEnabler né il `navigateToUrl:` callback o `navigateToUrl:useSVC:` chiamata di callback.

Mentre passa attraverso diversi reindirizzamenti, l&#39;applicazione deve monitorare l&#39;attività del `UIWebView/WKWebView or SFSafariViewController `controlla e rileva il momento in cui carica un URL personalizzato specifico. Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che il flusso di logout è stato completato e che è sicuro chiudere il controller. Quando il controller carica questo URL personalizzato specifico, l&#39;applicazione deve chiudere il controller e chiamare AccessEnabler&#39;s `handleExternalURL:url `Metodo API. Nel caso in cui l&#39;applicazione debba utilizzare un `SFSafariViewController `controlla l’URL personalizzato specifico definito dalla `application's custom scheme` (ad esempio`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), altrimenti questo URL personalizzato specifico viene definito dalla `ADOBEPASS_REDIRECT_URL `costante (ovvero `adobepass://ios.app`).

Alla fine, AccessEnabler chiamerà il [`setAuthenticationStatus()`](http://tve.helpdocsonline.com/ios-tvos-api-reference$setAuthNStatus) callback con un codice di stato pari a 0, che indica il successo del flusso di logout.

**Nota:** Se l’utente ha effettuato l’accesso utilizzando Apple SSO, verrà attivato lo stato VSA203. In questo caso, all&#39;utente deve essere richiesto di disconnettersi anche dalle impostazioni di sistema. In caso contrario, al riavvio dell’applicazione si verificherà una nuova autenticazione.


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: avvia il flusso di logout</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[Torna all&#39;inizio...](#apis)

</br>

### getSelectedProvider {#getSelProv}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Utilizzare questo metodo per determinare il provider attualmente selezionato.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: determinare l'MVPD attualmente selezionato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:** [`selectedProvider:`](#selProv)

[Torna all&#39;inizio...](#apis)

</br>

### selectedProvider {#selProv}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler che fornisce informazioni sull&#39;MVPD attualmente selezionato all&#39;applicazione.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: informazioni sull'MVPD attualmente selezionato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri**:

- *mvpd*: oggetto contenente informazioni sull&#39;MVPD attualmente selezionato

**Attivazione da:** [`getSelectedProvider`](#getSelProv)

[Torna all&#39;inizio...](#apis)

</br>

### getMetadata: {#getMeta}

**File:** AccessEnabler/headers/AccessEnabler.h

**Descrizione:** Utilizzare questo metodo per recuperare le informazioni esposte come metadati dalla libreria AccessEnabler. L&#39;applicazione può accedere a questi dati fornendo un dizionario *key* parametro di input.

Sono disponibili due tipi di metadati per i programmatori:

- Metadati statici (Authentication token TTL, Authorization token TTL e Device ID) 
- Metadati utente (informazioni specifiche per l&#39;utente, ad esempio ID utente, codice postale); può essere passato da un MVPD a un dispositivo dell&#39;utente durante i flussi di autenticazione e autorizzazione)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata API: query di AccessEnabler per i metadati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri:**

- *keyDictionary*: una struttura dati del dizionario, con il seguente formato:
   - Se la chiave è `METADATA_OPCODE_KEY` e il valore è `METADATA_AUTHENTICATION`, quindi viene eseguita la query per ottenere il tempo di scadenza del token di autenticazione.
   - Se la chiave è `METADATA_OPCODE_KEY` e il valore è `METADATA_AUTHORIZATION` **e**\
      chiave `METADATA_RESOURCE_ID_KEY` e value è un particolare ID risorsa, quindi la query viene eseguita per ottenere la scadenza del token di autorizzazione associato alla risorsa specificata.
   - Se la chiave è `METADATA_OPCODE_KEY` e il valore è `METADATA_DEVICE_ID`, quindi viene eseguita la query per ottenere l’ID dispositivo corrente. Tieni presente che questa funzione è disabilitata per impostazione predefinita e che i programmatori devono contattare l’Adobe per informazioni relative all’abilitazione e alle tariffe.
   - Se la chiave è `METADATA_OPCODE_KEY` e il valore è `METADATA_USER_META` **e** chiave `METADATA_USER_META_KEY` e value è il nome dei metadati, quindi la query viene fatta per i metadati utente. Elenco dei tipi di metadati utente disponibili:
      - `zip` - Elenco dei codici postali
      - `householdID` - identificatore della famiglia. Nel caso in cui un MVPD non supporti conti secondari, questo sarà identico a `userID`.
      - `maxRating` - Una raccolta delle valutazioni massime dei genitori per l&#39;utente
      - `userID` - Identificatore utente. Se un MVPD supporta i sottoaccount e l&#39;utente non è l&#39;account principale, `userID` sarà diverso da `householdID.`
      - `channelID` - Elenco dei canali che un utente ha diritto di visualizzare.

   **Nota:** I metadati utente effettivi disponibili per un programmatore dipendono da ciò che un MVPD rende disponibile.  Questo elenco verrà espanso man mano che i nuovi metadati saranno resi disponibili e aggiunti al sistema di autenticazione Primetime.

**Callback attivato:** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**Ulteriori informazioni:** [Metadati utente](https://tve.helpdocsonline.com/user-metadata-v2)

[Torna all&#39;inizio...](#apis)

</br>

### presentTVProviderDialog {#presentTvDialog}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler dopo la chiamata di[getAuthentication()](#getAuthN) se il richiedente attuale supporta almeno un MVPD con supporto SSO.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: risultato dei flussi SSO</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v2.0+

**Parametri**:

- viewController: rappresenta la finestra di dialogo SSO di Apple. Questo viewController deve essere visualizzato sullo schermo.

**Attivazione da:** [`getAuthentication`](#getAuthN)

**Ulteriori informazioni:** [Accesso singolo iOS/tvOS](https://tve.helpdocsonline.com/ios-tvos-sdk-api-reference#)

[Torna all&#39;inizio...](#apis)

</br>

### dismissTVProviderDialog {#dismissTvDialog}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler dopo che l&#39;utente chiude la finestra di dialogo SSO di Apple.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: risultato dei flussi SSO</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v2.0+

**Parametri**:

- viewController: rappresenta la finestra di dialogo SSO di Apple. È necessario rimuovere ViewController dallo schermo.

**Attivazione da:** Azione utente

**Ulteriori informazioni:** [Accesso singolo iOS/tvOS](https://tve.helpdocsonline.com/ios-tvos-sdk-api-reference#)

 

[Torna all&#39;inizio...](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler che fornisce i metadati richiesti tramite un [`getMetadata:`](#getMeta) chiama.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: risultato della richiesta di recupero metadati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**Disponibilità:** v1.0+

**Parametri**:

- *metadati*: I metadati richiesti. Questo valore è un `NSString` nel caso di metadati statici (Authentication TTL, Authorization TTL, Device ID).  Si tratta di un oggetto complesso quando si richiedono metadati specifici per l’utente. Questo oggetto complesso è in genere la rappresentazione Objective-C di un payload JSON (ad esempio &#39;{&quot;street&quot;: &quot;Main Avenue&quot;, &quot;edifici&quot;: [&quot;150&quot;, &quot;320&quot;]}&#39; è tradotto in Objective-C come NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;building&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;)).   Oggetto JSON metadati di esempio:

```JSON
        {
            updated: 1334243471,
            encrypted: ["encryptedProp"],
            data: {
                zip: ["12345", "34567"],
                maxRating: { 
                    "MPAA": "PG-13",
                    "VCHIP": "TV-Y", 
                    "URL": "http://exam.pl/e/manage/ratings"
                },
                householdID: "3456",
                userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                channelID: ["channel-1", "channel-2"]
            }
```

- *cifrato*: valore booleano che specifica se i metadati recuperati sono crittografati o meno. Questo parametro è significativo solo per le richieste di metadati utente, non ha alcun significato per i metadati statici (ad esempio, Authentication TTL) che vengono sempre ricevuti non crittografati. Se questo parametro è impostato su true, spetta al programmatore ottenere il valore dei metadati utente non crittografati eseguendo una decrittografia RSA utilizzando la chiave privata di whitelisting (la stessa chiave privata utilizzata per la firma dell&#39;ID richiedente nel [`setRequestor:setSignedRequestorId:`](#setReq) e `setRequestor:setSignedRequestorId:serviceProviders: `chiamate).

- *key*: Chiave utilizzata per formulare la richiesta di recupero dei metadati.

- *argomenti*: Lo stesso dizionario passato al [`getMetadata:`](#getMeta) chiama. Viene fornito per consentire all’applicazione di corrispondere alle richieste con le risposte.

**Attivazione da:** [`getMetadata:`](#getMeta)

**Ulteriori informazioni:** [Metadati utente](https://tve.helpdocsonline.com/user-metadata-v2)


[Torna all&#39;inizio...](#apis)

</br>

### MVPD {#mvpd}

**File:** AccessEnabler/headers/model/MVPD.h

**Descrizione** Descrive l&#39;oggetto MVPD. Può essere utilizzato per ottenere informazioni sulle proprietà dell&#39;MVPD.

**Disponibilità:** v1.0+ [la proprietà boardingStatus è disponibile dalla versione v2.2] 

**Proprietà**:

- ID (NSString) - L&#39;ID MVPD.
- (NSString) displayName - Il nome MVPD. [Deve essere utilizzato per visualizzare nel selettore]
- (NSString) logoURL - L&#39;indirizzo del logo MVPD.
- (BOOL) enablePlatformServices - Se true, MVPD supporta servizi SSO come [Apple SSO](https://tve.helpdocsonline.com/ios-tvos-sdk-api-reference#).
- (NSString) boardingStatus - Può avere 3 valori:
   - nil - L&#39;MVPD non supporta l&#39;SSO di Apple.
   - PICKER - L&#39;MVPD può apparire nel selettore Apple, ma il flusso di autenticazione viene fatto per Adobe.
   - SUPPORTATO - L’MVPD è completamente supportato da Apple e utilizzerà il token SSO di Apple.

[Torna all&#39;inizio...](#apis)

</br>

## Tracciamento degli eventi {#tracking}

AccessEnabler attiva un callback aggiuntivo che non è necessariamente correlato ai flussi di adesione. Implementazione [`sendTrackingData()`](#sendTracking) la funzione di callback è opzionale, ma consente all&#39;applicazione di tenere traccia di eventi specifici e di compilare statistiche quali il numero di tentativi di autenticazione/autorizzazione riusciti/non riusciti. 

### sendTrackingData:forEventType: {#sendTracking}

**File:** AccessEnabler/headers/EntitlementDelegate.h

**Descrizione** Callback attivato da AccessEnabler segnalando all&#39;applicazione il verificarsi di vari eventi come il completamento/il fallimento dei flussi di autenticazione/autorizzazione. Con Primetime Authentication 1.6, il tipo di dispositivo, il tipo di client AccessEnabler e il sistema operativo sono segnalati da [`sendTrackingData()`](#sendTracking). La [`sendTrackingData()`](#sendTracking) callback rimane compatibile con le versioni precedenti.

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Callback: eventi di tracciamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event; </code></pre></td>
</tr>
</tbody>
</table>

 

**Disponibilità:** v1.0+

**Nota:** Il tipo di dispositivo e il sistema operativo sono derivati dall&#39;utilizzo di una libreria Java pubblica (<http://java.net/projects/user-agent-utils>) e la stringa dell&#39;agente utente. Tieni presente che queste informazioni vengono fornite solo come modo approssimativo per suddividere le metriche operative in categorie di dispositivi, ma che l’Adobe non può assumersi alcuna responsabilità per i risultati errati. Utilizza di conseguenza la nuova funzionalità.

- Valori possibili per il tipo di dispositivo:
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- Valori possibili per il tipo di client AccessEnabler:
   - `flash`
   - `html5`
   - `ios`
   - `android`


**Parametri**:

- *event*: il codice dell’evento che viene tracciato. Esistono tre tipi di eventi di tracciamento possibili:
   - **authorizationDetection:** ogni volta che viene restituita una richiesta di token di autorizzazione (l&#39;evento è `TRACKING_AUTHORIZATION`)
   - **authenticationDetection:** ogni volta che si verifica un controllo di autenticazione (l&#39;evento è `TRACKING_AUTHENTICATION`)
   - **mvpdSelection:** quando l&#39;utente seleziona un MVPD nel modulo di selezione MVPD (l&#39;evento è `TRACKING_GET_SELECTED_PROVIDER`)
- *dati*: dati aggiuntivi associati all’evento segnalato. Questi dati vengono presentati sotto forma di un elenco di valori.

**Attivazione da:** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

Istruzioni per l’interpretazione dei valori nel *dati* array:

- Per trackingEventType `TRACKING_AUTHENTICATION:`
   - **0** - Se la richiesta del token è riuscita (true/false) e se ha avuto esito positivo:
   - **1** - Stringa ID MVPD
   - **2** - GUID (con hash md5)
   - **3** - Token già presente nella cache (true/false)
   - **4** - Tipo di dispositivo
   - **5** - Tipo di client AccessEnabler
   - **6** - Tipo di sistema operativo

- Per trackingEventType `TRACKING_AUTHORIZATION:`
   - **0** - Se la richiesta del token è riuscita (true/false) e se ha avuto esito positivo:
   - **1** - ID MVPD
   - **2** - GUID (con hash md5)
   - **3** - Token già presente nella cache (true/false)
   - **4** - Errore
   - **5** - Dettagli
   - **6** - Tipo di dispositivo
   - **7** - Tipo di client AccessEnabler
   - **8** - Tipo di sistema operativo
- Per trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   - **0** - ID dell&#39;MVPD attualmente selezionato
   - **1** - Tipo di dispositivo
   - **2** - Tipo di client AccessEnabler
   - **3** - Tipo di sistema operativo

</br>

## Informazioni correlate {#related}

- [Guida di riferimento per l’integrazione di iOS](/help/authentication/iostvos-sdk-cookbook.md)
- [Panoramica tecnica di iOS](/help/authentication/iostvos-sdk-overview.md)
- [Flusso di adesione](https://tve.helpdocsonline.com/entitlement-flow)
- [Tracciamento dei dati nell’autenticazione di Primetime](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)
