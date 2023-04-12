---
title: Riferimento API client nativo di Amazon FireOS
description: Riferimento API client nativo di Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---


# Riferimento API client nativo di Amazon FireOS {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#intro}

Questo documento descrive i metodi e i callback esposti dall’SDK Amazon FireOS per l’autenticazione Adobe Primetime, supportati con l’autenticazione Adobe Primetime.</span> I metodi e le funzioni di callback qui descritti sono definiti nei file di intestazione AccessEnabler.h e EntitlementDelegate.h.

Fai riferimento a <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> per l&#39;SDK Amazon FireOS AccessEnabler più recente. 

**Nota:** Il team di autenticazione di Adobe Primetime ti incoraggia a utilizzare solo l’autenticazione di Adobe Primetime *pubblico* API:

- API pubbliche disponibili *e completamente testato* su tutti i tipi di client supportati. Per qualsiasi funzionalità pubblica, assicuriamo che ogni tipo di client abbia una versione corrispondente dei metodi associati.
- Le API pubbliche devono essere il più stabili possibile, per supportare la compatibilità con le versioni precedenti e garantire che le integrazioni dei partner non vengano interrotte. Tuttavia, per *non*- API pubbliche, ci riserviamo il diritto di modificare la loro firma in qualsiasi momento futuro. Se incontri un flusso particolare che non può essere supportato tramite una combinazione delle chiamate API pubbliche di autenticazione di Adobe Primetime correnti, l’approccio migliore è farcelo sapere. Tenendo conto delle tue esigenze, possiamo modificare le API pubbliche e fornire una soluzione stabile che prosegua.

## API SDK Amazon FireOS {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigaToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthorizedResources](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [disconnessione](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**Descrizione:** Crea un&#39;istanza dell&#39;oggetto Access Enabler. Deve essere presente una singola istanza di Access Enabler per ogni istanza di applicazione.

| Chiamata API: costruttore |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**Disponibilità:** v3.0+


**Parametri:**

- *appContext*: Contesto dell&#39;applicazione Amazon Fire OS.
- softwareStatement
- redirectUrl : in caso di FireOS, il valore del parametro verrà ignorato e impostato su predefinito : adobepass://android.app
- env_url: per il test utilizzando l&#39;ambiente di staging di Adobe, env\_url può essere impostato su &quot;sp.auth-staging.adobe.com&quot;

**Obsoleto:**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**Descrizione:** Stabilisce l&#39;identità del programmatore. A ciascun programmatore viene assegnato un ID univoco al momento della registrazione con Adobe per il sistema di autenticazione Adobe Primetime. Questa impostazione deve essere eseguita una sola volta durante il ciclo di vita dell&#39;applicazione.

La risposta del server contiene un elenco di MVPD insieme ad alcune informazioni di configurazione collegate all&#39;identità del programmatore. La risposta del server viene utilizzata internamente dal codice di Access Enabler . Solo lo stato dell&#39;operazione (ovvero SUCCESS/FAIL) viene presentato all&#39;applicazione tramite il callback setRequestorComplete().

Se la *url* Il parametro non viene utilizzato, la chiamata di rete risultante esegue il targeting dell&#39;URL predefinito del provider di servizi: ambiente di rilascio/produzione di Adobe.

Se viene fornito un valore per *url* , la chiamata di rete risultante esegue il targeting di tutti gli URL forniti nel *url* parametro . Tutte le richieste di configurazione vengono attivate simultaneamente in thread separati. Il primo risponditore ha la precedenza quando si compila l&#39;elenco degli MVPD. Per ogni MVPD nell&#39;elenco, Access Enabler ricorda l&#39;URL del provider di servizi associato. Tutte le richieste di adesione successive vengono indirizzate all&#39;URL associato al provider di servizi che è stato abbinato all&#39;MVPD di destinazione durante la fase di configurazione.

| Chiamata API: configurazione richiedente |
| --- |
| ```public void setRequestor(String requestorId)``` |


**Disponibilità:**v 3.0+


| Chiamata API: configurazione richiedente |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilità:** v3.0+


**Parametri:**

- *requestorID*: ID univoco associato al programmatore. Passa l&#39;ID univoco assegnato da Adobe al tuo sito la prima volta che ti sei registrato con il servizio di autenticazione Adobe Primetime.
- *url*: Parametro facoltativo; per impostazione predefinita, viene utilizzato il provider di servizi Adobe (http://sp.auth.adobe.com/). Questo array consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). È possibile utilizzarlo per specificare più istanze del provider di servizi di autenticazione Adobe Primetime. In questo modo, l&#39;elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al fornitore di servizi più veloce; cioè, il fornitore che ha risposto per primo e che supporta quel MVPD.

**Callback attivato:** `setRequestorComplete()`

 

**Obsoleto:**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**Descrizione:** Callback attivato da Access Enabler che informa l&#39;applicazione del completamento della fase di configurazione. Questo è un segnale che l’app può iniziare a emettere richieste di adesione. L&#39;applicazione non può emettere richieste di adesione fino al completamento della fase di configurazione.

| Callback: configurazione del richiedente completata |
| --- |
| ```public void setRequestorComplete(int status)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *status*: Può assumere uno dei seguenti valori:
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - fase di configurazione completata
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - fase di configurazione non riuscita

**Attivazione da:** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**Descrizione:** Configura le opzioni SDK globali. Accetta un **Mappa\&lt;string string=&quot;&quot;>** come argomento. I valori della mappa verranno passati al server insieme a ogni chiamata di rete effettuata dall&#39;SDK.

I valori verranno passati al server indipendentemente dal flusso corrente (autenticazione/autorizzazione). Se si desidera modificare i valori, è possibile chiamare questo metodo in qualsiasi momento.

 

| Chiamata API: setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**Disponibilità:** v3.0+

**Parametri:**

- *options*: Una mappa\&lt;string string=&quot;&quot;> contenente opzioni SDK globali. Sono attualmente disponibili le seguenti opzioni:
   - **applicationProfile** - Può essere utilizzato per effettuare configurazioni server basate su questo valore.
   - **ap\_vi** - Il Marketing Cloud visitorID. Questo valore può essere successivamente utilizzato per i rapporti di analisi avanzati.
   - **device\_info** - Informazioni sul dispositivo come descritto in **Passaggio della libreria di informazioni sul dispositivo**

</br>

### checkAuthentication {#checkAuthN}

**Descrizione:** Controlla lo stato di autenticazione. A tale scopo, cerca un token di autenticazione valido nello spazio di archiviazione locale dei token. La chiamata di questo metodo non esegue chiamate di rete. Viene utilizzato dall’applicazione per eseguire una query sullo stato di autenticazione dell’utente e aggiornare di conseguenza l’interfaccia utente (ovvero per aggiornare l’interfaccia utente di accesso/disconnessione). Lo stato di autenticazione viene comunicato all’applicazione tramite il [*setAuthenticationStatus()*](#setAuthNStatus) callback.

Se un MVPD supporta la funzione &quot;Authentication per Requestor&quot;, è possibile memorizzare più token di autenticazione su un dispositivo. 

| Chiamata API: verifica stato autenticazione |
| --- |
| ```public void checkAuthentication()``` |

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**Descrizione:** Avvia il flusso di lavoro di autenticazione completo. Inizia controllando lo stato di autenticazione. Se non è già autenticato, viene avviato il computer dello stato del flusso di autenticazione:

- Se l&#39;ultimo tentativo di autenticazione ha avuto esito positivo, la fase di selezione MVPD viene saltata e un controllo WebView presenterà all&#39;utente la pagina di accesso dell&#39;MVPD.
- Se l&#39;ultimo tentativo di autenticazione non ha avuto esito positivo o se l&#39;utente si è disconnesso in modo esplicito, la [*displayProviderDialog()*](#displayProviderDialog) viene attivato il callback. L&#39;applicazione utilizza questo callback per visualizzare l&#39;interfaccia utente di selezione MVPD. È inoltre necessario che l’app riprenda il flusso di autenticazione informando la libreria di Access Enabler sulla selezione MVPD dell’utente tramite la [setSelectedProvider()](#setSelectedProvider) metodo .

Se un MVPD supporta la funzione &quot;Authentication per Requestor&quot;, è possibile memorizzare più token di autenticazione su un dispositivo (uno per programmatore).

Infine, lo stato di autenticazione viene comunicato all&#39;applicazione tramite il *setAuthenticationStatus()* callback.

| Chiamata API: avvia il flusso di autenticazione |
| --- |
| ```public void getAuthentication()``` |

**Disponibilità:** v1.0+

| Chiamata API: avvia il flusso di autenticazione |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *forceAuthn*: Flag che specifica se il flusso di autenticazione deve essere avviato, indipendentemente dal fatto che l&#39;utente sia già autenticato o meno.
- *dati*: Mappa costituita da coppie chiave-valore da inviare al servizio pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK.

**Callback attivato:** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**Descrizione** Callback attivato da Access Enabler per informare l&#39;applicazione che è necessario creare un&#39;istanza degli elementi dell&#39;interfaccia utente appropriati per consentire all&#39;utente di selezionare l&#39;MVPD desiderato. Il callback fornisce un elenco di oggetti MVPD con informazioni aggiuntive che possono aiutare a creare correttamente il pannello dell’interfaccia utente di selezione (come l’URL che punta al logo dell’MVPD, il nome visualizzato descrittivo, ecc.)

Una volta che l&#39;utente ha selezionato il MVPD desiderato, l&#39;applicazione di livello superiore è necessaria per riprendere il flusso di autenticazione chiamando *setSelectedProvider()* e trasmettendolo l&#39;ID dell&#39;MVPD corrispondente alla selezione dell&#39;utente.\
 

| **Callback: visualizzare l&#39;interfaccia utente di selezione MVPD** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**Disponibilità:** v1.0+

**Parametri**:

- *mvpds*: Elenco di oggetti MVPD che contengono informazioni relative a MVPD che l&#39;applicazione può utilizzare per creare gli elementi dell&#39;interfaccia utente di selezione MVPD.

**Attivazione da:** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**Descrizione:** Questo metodo viene chiamato dall&#39;applicazione per informare Access Enabler della selezione MVPD dell&#39;utente. Al passaggio *null* come parametro, Access Enabler reimposta l&#39;MVPD corrente su un valore null.

| **Chiamata API: imposta il provider attualmente selezionato** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**Disponibilità:**v 1.0+

**Parametri:** Nessuno

**Callback attivato:** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navigaToUrl {#navigagteToUrl}

**Descrizione:** Callback attivato da Access Enabler sull&#39;SDK di Android. Deve essere ignorato nell’SDK Amazon FireOS.

| **Callback: visualizzare la pagina di accesso MVPD** |
| --- |
| ```public void navigateToUrl(String url)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *url*: L&#39;URL che punta alla pagina di accesso dell&#39;MVPD

**Attivazione da:** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**Descrizione:** Completa il flusso di autenticazione richiedendo il token di autenticazione dal server back-end. 

| **Chiamata API: recuperare il token di autenticazione** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *cookie*: Cookie impostati sul dominio di destinazione (consulta l’applicazione demo nell’SDK per un’implementazione di riferimento).

**Callback attivato:** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**Descrizione:** Callback attivato da Access Enabler che informa l&#39;applicazione dello stato dell&#39;autenticazione. Ci sono molti luoghi in cui il flusso di autenticazione può fallire, sia a causa dell&#39;interazione dell&#39;utente o a causa di altri scenari imprevisti (ad esempio problemi di connettività di rete, ecc.). Questo callback informa l&#39;applicazione dello stato di successo/errore dell&#39;autenticazione, fornendo anche informazioni aggiuntive sul motivo dell&#39;errore, se necessario.

Questo callback segnala anche quando il flusso di logout è completo.

| **Callback: segnalare lo stato del flusso di autenticazione** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *status*: Può assumere uno dei seguenti valori:
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - flusso di autenticazione completato
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - flusso di autenticazione non riuscito
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT` - logout
- *codice*: Motivo dello stato di presentazione. Se *status* è `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`, quindi *codice* è una stringa vuota (ad esempio, definita dalla `AccessEnabler.USER_AUTHENTICATED` costante). Se non è autenticato, questo parametro può assumere uno dei seguenti valori:
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR` - Utente non autenticato. In risposta al *checkAuthentication()* chiamata del metodo quando non è presente un token di autenticazione valido nella cache del token locale.
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler ha reimpostato la macchina dello stato di autenticazione dopo il passaggio dell&#39;applicazione di livello superiore *null* a `setSelectedProvider()` per interrompere il flusso di autenticazione.  Presumibilmente l&#39;utente ha annullato il flusso di autenticazione (cioè ha premuto il pulsante &quot;Indietro&quot;).
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR` - Il flusso di autenticazione non è riuscito a causa di motivi quali l&#39;indisponibilità della rete o l&#39;utente ha annullato esplicitamente il flusso di autenticazione.
   - `AccessEnabler.LOGOUT` - L’utente non viene autenticato a causa di un’azione di logout. 

**Attivazione da:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per determinare se l&#39;utente è già autorizzato a visualizzare risorse protette specifiche. Lo scopo principale di questo metodo è quello di recuperare informazioni da utilizzare per decorare l’interfaccia utente (ad esempio, per indicare lo stato di accesso con le icone di blocco e sblocco).

| **Chiamata API: imposta il provider attualmente selezionato** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Disponibilità:** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> La `resources` parametro è una matrice di risorse per le quali è necessario controllare l&#39;autorizzazione.** Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa nel `getAuthorization()` chiamare, cioè, dovrebbe essere un valore concordato stabilito tra il programmatore e il MVPD o un frammento RSS media.

**Callback attivato:** `preauthorizedResources()`

</br>

### preauthorizedResources {#preauthResources}

**Descrizione:** Callback attivato da checkPreauthorizedResources(). Fornisce un elenco delle risorse che l&#39;utente è già autorizzato a visualizzare.

| **Chiamata API: imposta il provider attualmente selezionato** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Disponibilità:**v 1.0+

**Parametri:** La `resources` è un array di risorse per le quali l&#39;utente è già autorizzato a visualizzare.

**Attivazione da:** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per controllare lo stato dell&#39;autorizzazione. Inizia controllando prima lo stato di autenticazione. Se non autenticato, il *setTokenRequestFailed()* viene attivato il callback e il metodo esce. Se l&#39;utente è autenticato, attiva anche il flusso di autorizzazione. Vedi i dettagli *getAuthorization()* metodo .

| **Chiamata API: verifica lo stato dell&#39;autorizzazione** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**Disponibilità:** v1.0+

| **Chiamata API: verifica lo stato dell&#39;autorizzazione** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *resourceId*: ID della risorsa per la quale l’utente richiede l’autorizzazione.
- *dati*: Mappa costituita da coppie chiave-valore da inviare al servizio pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK.

**Callback attivato:** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per avviare il flusso di autorizzazione. Se l’utente non è già autenticato, avvia anche il flusso di autenticazione. Se l&#39;utente viene autenticato, Access Enabler continua a emettere richieste per il token di autorizzazione (se non è presente alcun token di autorizzazione valido nella cache dei token locali) e per il token multimediale di breve durata. Una volta ottenuto il token multimediale breve, il flusso di autorizzazione viene considerato completo. La *setToken()* il callback viene attivato e il token multimediale breve viene consegnato come parametro all&#39;applicazione. Se per qualsiasi motivo l&#39;autorizzazione non riesce, il *tokenRequestFailed()* viene attivato il callback e vengono forniti il codice di errore e i dettagli.

| **Chiamata API: avvia il flusso di autorizzazione** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**Disponibilità:** v1.0+

| **Chiamata API: avvia il flusso di autorizzazione** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *resourceId*: ID della risorsa per la quale l’utente richiede l’autorizzazione.
- *dati*: Mappa costituita da coppie chiave-valore da inviare al servizio pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l&#39;SDK. 

**Callback attivato:** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **Callback aggiuntivi attivati**  <br>Questo metodo può anche attivare i seguenti callback (se viene avviato anche il flusso di autenticazione): _setAuthenticationStatus()_, _displayProviderDialog()_ |

**NOTA: Utilizza checkAuthorization() invece di getAuthorization() quando possibile. Il metodo getAuthorization() avvia un flusso di autenticazione completo (se l’utente non è autenticato) che potrebbe comportare un’implementazione complicata da parte del programmatore.**

</br>

### setToken {#setToken}

**Descrizione:** Callback attivato da Access Enabler che informa l&#39;applicazione che il flusso di autorizzazione è stato completato correttamente. Anche il token multimediale di breve durata viene consegnato come parametro.

| **Callback: flusso di autorizzazione completato** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**Disponibilità:**v 1.0+

**Parametri:**

- *token*: Il token multimediale di breve durata
- *resourceId*: Risorsa per la quale è stata ottenuta l&#39;autorizzazione

**Attivazione da:** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**Descrizione:** Callback attivato da Access Enabler che informa l&#39;applicazione di livello superiore che il flusso di autorizzazione non è riuscito.

| **Callback: flusso di autorizzazione non riuscito** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *resourceId*: Risorsa per la quale è stata ottenuta l&#39;autorizzazione
- *errorCode*: Codice di errore associato allo scenario di errore. Valori possibili:
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR` - Impossibile autorizzare l&#39;utente per la risorsa specificata
- *errorDescription*: Ulteriori dettagli sullo scenario di errore. Se questa stringa descrittiva non è disponibile per alcun motivo, l&#39;autenticazione Adobe Primetime invia una stringa vuota >**(&quot;&quot;)**.  Questa stringa può essere utilizzata da un MVPD per trasmettere messaggi di errore personalizzati o messaggi relativi alle vendite. Ad esempio, se a un utente iscritto viene negata l&#39;autorizzazione per una risorsa, l&#39;MVPD potrebbe inviare un messaggio come: &quot;Al momento non hai accesso a questo canale nel tuo pacchetto. Se desideri aggiornare il tuo pacchetto clicca qui.&quot; Il messaggio viene passato dall&#39;autenticazione Adobe Primetime tramite questo callback al programmatore, che ha l&#39;opzione di visualizzarlo o ignorarlo. L’autenticazione Adobe Primetime può inoltre utilizzare questo parametro per fornire la notifica della condizione che potrebbe aver generato un errore. Ad esempio, &quot;Errore di rete durante la comunicazione con il servizio di autorizzazione del provider&quot;.

**Attivazione da:** `checkAuthorization(), getAuthorization()`

</br>

### disconnessione {#logout}

**Descrizione:** Utilizza questo metodo per avviare il flusso di logout. La disconnessione è il risultato di una serie di operazioni di reindirizzamento HTTP a causa del fatto che l&#39;utente deve essere disconnesso sia dai server di autenticazione Adobe Primetime che dai server MVPD. 

| **Chiamata API: avvia il flusso di logout** |
| --- |
| ```public void logout()``` |

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:** Nessuno

</br>

### getSelectedProvider {#getSelectedProvider}

**Descrizione:** Utilizzare questo metodo per determinare il provider attualmente selezionato.

| **Chiamata API: determinare l&#39;MVPD attualmente selezionato** |
| --- |
| ```public void getSelectedProvider()``` |

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivato:** `selectedProvider()`

</br>

### selectedProvider {#selectedProvider}

**Descrizione:** Callback attivato da Access Enabler che fornisce informazioni sull&#39;MVPD attualmente selezionato all&#39;applicazione.

| **Callback: informazioni sull&#39;MVPD attualmente selezionato** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *mvpd*: Oggetto contenente informazioni sull&#39;MVPD attualmente selezionato

**Attivazione da:** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**Descrizione:** Utilizzare questo metodo per recuperare le informazioni esposte come metadati dalla libreria di Access Enabler. L&#39;applicazione può accedere a queste informazioni fornendo un oggetto composito MetadataKey.

| **Chiamata API: query di AccessEnabler per i metadati** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**Disponibilità:** v1.0+

Sono disponibili due tipi di metadati per i programmatori:

- Metadati statici (Authentication token TTL, Authorization token TTL e Device ID) 
- Metadati utente (informazioni specifiche per l&#39;utente, ad esempio ID utente e CAP; trasmesse da un MVPD al dispositivo di un utente durante i flussi di autenticazione e/o autorizzazione)

**Parametri:**

- *metadataKey*: Una struttura di dati che racchiude una variabile chiave e args, con il seguente significato:
   - Se la chiave è `METADATA_KEY_TTL_AUTHN` quindi viene eseguita la query per ottenere il tempo di scadenza del token di autenticazione.
   - Se la chiave è `METADATA_KEY_TTL_AUTHZ` e args contiene un oggetto SerializableNameValuePair con nome = `METADATA_ARG_RESOURCE_ID` e value = `[resource_id]`, quindi viene eseguita la query per ottenere la data di scadenza del token di autorizzazione associato alla risorsa specificata.
   - Se la chiave è `METADATA_KEY_DEVICE_ID` quindi viene eseguita la query per ottenere l&#39;id dispositivo corrente. Tieni presente che questa funzione è disabilitata per impostazione predefinita e che i programmatori devono contattare l’Adobe per informazioni relative all’abilitazione e alle tariffe.
   - Se la chiave è `METADATA_KEY_USER_META` e args contiene un oggetto SerializableNameValuePair con nome = `METADATA_KEY_USER_META` e value = `[metadata_name]`, quindi viene eseguita la query per i metadati utente. Elenco corrente dei tipi di metadati utente disponibili:
      - `zip` - Codice postale
      - `householdID` - identificatore della famiglia. Se un MVPD non supporta i sottoconti, sarà identico a `userID`.
      - `maxRating` - Valutazione massima per i genitori dell&#39;utente
      - `userID` - Identificatore utente. Se un MVPD supporta i sottoaccount e l&#39;utente non è l&#39;account principale,
      - `channelID` - Elenco dei canali che l&#39;utente ha diritto di visualizzare

I metadati utente effettivi disponibili per un programmatore dipendono da ciò che un MVPD rende disponibile.  Questo elenco verrà ulteriormente esteso man mano che i nuovi metadati saranno resi disponibili e aggiunti al sistema di autenticazione Adobe Primetime.

**Callback attivato:** [`setMetadataStatus()`](#setMetadaStatus)

**Ulteriori informazioni:** [Metadati utente](#setmetadatastatus)

</br>

### setMetadataStatus {#setMetadaStatus}

**Descrizione:** Callback attivato da Access Enabler che distribuisce i metadati richiesti tramite un *getMetadata()* chiama.

| **Callback: risultato della richiesta di recupero metadati** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *key*: L&#39;oggetto MetadataKey contenente la chiave per la quale viene richiesto il valore di metadati e i parametri associati (vedere applicazione demo per un&#39;implementazione di riferimento).
- *risultato*: Un oggetto composito contenente i metadati richiesti. L’oggetto presenta i campi seguenti:
   - *simpleResult*: un valore String che rappresenta il valore dei metadati quando è stata effettuata la richiesta per Authentication TTL, Authorization TTL o Device ID. Questo valore è nullo se è stata effettuata la richiesta per i metadati utente.

   - *userMetadataResult*: un oggetto che contiene la rappresentazione Java di un payload per metadati utente JSON. Ad esempio:

      ```json
      {
      "street": "Main Avenue",
      "buildings": ["150", "320"]
      }
      ```

      è tradotto in Java come: 

      ```java
      Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
      ```

      **La struttura effettiva degli oggetti metadati utente è simile alla seguente:**

      ```json
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
      }
      ```
 

Questo valore è nullo quando è stata effettuata la richiesta per metadati semplici (Authentication TTL, Authorization TTL o Device ID).

- *cifrato*: Valore booleano che specifica se i metadati recuperati sono crittografati o meno. Questo parametro è significativo solo per le richieste di metadati utente, non ha alcun significato per i metadati statici (ad esempio, Authentication TTL) che vengono sempre ricevuti non crittografati. Se questo parametro è impostato su True, spetta al programmatore ottenere il valore dei metadati utente non crittografati eseguendo una decrittografia RSA utilizzando la chiave privata nella whitelist (la stessa chiave privata utilizzata per la firma del requestor id nel [`setRequestor`](#setRequestor) chiamare).

**Attivazione da:** [`getMetadata()`](#getMetadata)

**Ulteriori informazioni:** [Metadati utente](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**Descrizione:** Utilizzare questo metodo per recuperare la versione corrente di AccessEnabler  

| **Chiamata API: ottenere la versione di AccessEnabler** |
| --- |
| ```public static String getVersion()``` |

## Tracciamento degli eventi {#tracking}

Access Enabler attiva un callback aggiuntivo che non è necessariamente correlato ai flussi di adesione. Implementazione della funzione di callback di tracciamento degli eventi denominata *sendTrackingData()* è facoltativo, ma consente all’applicazione di tenere traccia di eventi specifici e di compilare statistiche quali il numero di tentativi di autenticazione/autorizzazione riusciti/non riusciti. Di seguito sono riportate le specifiche per *sendTrackingData()* callback:

### sendTrackingData {#sendTrackingData}

**Descrizione:** Callback attivato dal servizio Access Enabler segnalando all&#39;applicazione il verificarsi di vari eventi come il completamento/il fallimento dei flussi di autenticazione/autorizzazione. Il tipo di dispositivo, il tipo di client di Access Enabler e il sistema operativo vengono segnalati anche da sendTrackingData().

>[!WARNING]
>
> Il tipo di dispositivo e il sistema operativo sono derivati dall&#39;utilizzo di una libreria Java pubblica (http://java.net/projects/user-agent-utils) e della stringa dell&#39;agente utente. Tieni presente che queste informazioni vengono fornite solo come modo approssimativo per suddividere le metriche operative in categorie di dispositivi, ma che l’Adobe non può assumersi alcuna responsabilità per i risultati errati. Utilizza di conseguenza la nuova funzionalità.

- Valori possibili per il tipo di dispositivo:
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- Valori possibili per il tipo di client di Access Enabler:
   - `flash`
   - `html5`
   - `ios`
   - `tvos`
   - `android`
   - `firetv`

| Callback: eventi di tracciamento |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *event*: l&#39;evento di cui si sta eseguendo il tracciamento. Esistono tre tipi di eventi di tracciamento possibili:
   - **authorizationDetection:** ogni volta che viene restituita una richiesta di token di autorizzazione (il tipo di evento è `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection:** ogni volta che si verifica un controllo di autenticazione (il tipo di evento è `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** quando l&#39;utente seleziona un MVPD nel modulo di selezione MVPD (il tipo di evento è `EVENT_MVPD_SELECTION`)
- *dati*: dati aggiuntivi associati all’evento segnalato. Questi dati vengono presentati sotto forma di un elenco di valori.

Di seguito sono riportate le istruzioni per interpretare i valori nel *dati* array:

- Per il tipo di evento *`EVENT_AUTHN_DETECTION`:*
   - **0** - Se la richiesta del token è riuscita (true/false) e se quanto sopra è vero:
   - **1** - Stringa ID MVPD
   - **2** - GUID (con hash md5)
   - **3** - Token già presente nella cache (true/false)
   - **4** - Tipo di dispositivo
   - **5** - Access Enabler, tipo di client
   - **6** - Tipo di sistema operativo

- Per il tipo di evento `EVENT_AUTHZ_DETECTION`
   - **0** - Se la richiesta del token è riuscita (true/false) e se ha avuto esito positivo:
   - **1** - ID MVPD
   - **2** - GUID (con hash md5)
   - **3** - Token già presente nella cache (true/false)
   - **4** - Errore
   - **5** - Dettagli
   - **6** - Tipo di dispositivo
   - **7** - Access Enabler, tipo di client
   - **8** - Tipo di sistema operativo

- Per il tipo di evento `EVENT_MVPD_SELECTION`
   - **0** - ID dell&#39;MVPD attualmente selezionato
   - **1** - Tipo di dispositivo
   - **2** - Access Enabler, tipo di client
   - **3** - Tipo di sistema operativo

**Attivazione da:** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
