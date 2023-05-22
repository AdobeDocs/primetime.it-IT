---
title: Riferimento API client nativo Amazon FireOS
description: Riferimento API client nativo Amazon FireOS
exl-id: 8ac9f976-fd6b-4b19-a80d-49bfe57134b5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---

# Riferimento API client nativo Amazon FireOS {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#intro}

Questo documento descrive i metodi e i callback esposti dall’SDK Amazon FireOS per l’autenticazione Adobe Primetime, supportati con l’autenticazione Adobe Primetime.</span> I metodi e le funzioni di callback qui descritti sono definiti nei file di intestazione AccessEnabler.h e EntitlementDelegate.h.

Fare riferimento a <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> per la versione più recente dell’SDK di Amazon FireOS AccessEnabler. 

**Nota:** Il team di autenticazione di Adobe Primetime ti incoraggia a utilizzare solo l’autenticazione di Adobe Primetime *pubblico* API:

- Sono disponibili API pubbliche *e completamente testato* su tutti i tipi di client supportati. Per qualsiasi funzione pubblica, ci assicuriamo che ogni tipo di client abbia una versione corrispondente dei metodi associati.
- Le API pubbliche devono essere il più stabili possibile, per supportare la compatibilità con le versioni precedenti e garantire che le integrazioni dei partner non si interrompano. Tuttavia, per *non*-API pubbliche, ci riserviamo il diritto di cambiare la loro firma in qualsiasi momento futuro. Se incontri un flusso particolare che non può essere supportato tramite una combinazione delle chiamate API pubbliche di autenticazione di Adobe Primetime, l’approccio migliore è quello di farcelo sapere. Tenendo conto delle tue esigenze, possiamo modificare le API pubbliche e fornire una soluzione stabile.

## API SDK di Amazon FireOS {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [risorse preautorizzate](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [logout](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**Descrizione:** Crea istanze dell&#39;oggetto Access Enabler. Deve essere presente una singola istanza di Access Enabler per ogni istanza dell&#39;applicazione.

| Chiamata API: costruttore |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**Disponibilità:** v3.0+


**Parametri:**

- *appContext*: contesto dell’applicazione Amazon Fire OS.
- softwareStatement
- redirectUrl : in caso di FireOS, il valore del parametro verrà ignorato e impostato sul valore predefinito : adobepass://android.app
- env_url: per eseguire test utilizzando l’ambiente di staging Adobe, env\_url può essere impostato su &quot;sp.auth-staging.adobe.com&quot;

**Obsoleto:**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```
 

### setRequestor {#setRequestor}

**Descrizione:** Stabilisce l&#39;identità del programmatore. A ciascun programmatore viene assegnato un ID univoco al momento della registrazione all’Adobe per il sistema di autenticazione di Adobe Primetime. Questa impostazione deve essere eseguita una sola volta durante il ciclo di vita dell&#39;applicazione.

La risposta del server contiene un elenco di MVPD insieme ad alcune informazioni di configurazione collegate all&#39;identità del programmatore. La risposta del server viene utilizzata internamente dal codice di Access Enabler. Solo lo stato dell’operazione (ovvero SUCCESS/FAIL) viene presentato all’applicazione tramite il callback setRequestorComplete().

Se il *url* non viene utilizzato, la chiamata di rete risultante esegue il targeting dell’URL predefinito del fornitore di servizi: l’ambiente Adobe Release/Production.

Se per il campo *url* , la chiamata di rete risultante esegue il targeting di tutti gli URL forniti nel *url* parametro. Tutte le richieste di configurazione vengono attivate contemporaneamente in thread separati. Il primo responder ha la precedenza quando si compila l’elenco degli MVPD. Per ogni MVPD nell&#39;elenco, Access Enabler ricorda l&#39;URL del provider di servizi associato. Tutte le richieste di adesione successive vengono indirizzate all’URL associato al provider di servizi che è stato associato all’MVPD di destinazione durante la fase di configurazione.

| Chiamata API: configurazione richiedente |
| --- |
| ```public void setRequestor(String requestorId)``` |


**Disponibilità:**v 3.0+


| Chiamata API: configurazione richiedente |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Disponibilità:** v3.0+


**Parametri:**

- *requestorID*: ID univoco associato al programmatore. Passa l’ID univoco assegnato da Adobe al sito alla prima registrazione al servizio di autenticazione di Adobe Primetime.
- *url*: parametro facoltativo; per impostazione predefinita, viene utilizzato il provider di servizi Adobe (http://sp.auth.adobe.com/). Questo array consente di specificare gli endpoint per i servizi di autenticazione e autorizzazione forniti da Adobe (a scopo di debug possono essere utilizzate istanze diverse). È possibile utilizzare questa opzione per specificare più istanze del provider di servizi di autenticazione di Adobe Primetime. In tal caso, l&#39;elenco MVPD è composto dagli endpoint di tutti i fornitori di servizi. Ogni MVPD è associato al provider di servizi più veloce, ovvero il provider che ha risposto per primo e che supporta tale MVPD.

**Callback attivati:** `setRequestorComplete()`

 

**Obsoleto:**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```
 
</br>


### setRequestorComplete {#setRequestorComplete}

**Descrizione:** Callback attivato dall&#39;Access Enabler che informa l&#39;applicazione del completamento della fase di configurazione. Questo è un segnale che l’app può iniziare a emettere richieste di adesione. L’applicazione non può inviare richieste di adesione fino al completamento della fase di configurazione.

| Callback: configurazione richiedente completata |
| --- |
| ```public void setRequestorComplete(int status)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *stato*: può assumere uno dei seguenti valori:
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - fase di configurazione completata
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - fase di configurazione non riuscita

**Attivato da:** `setRequestor()`

</br> 


### setOptions {#fire_setOption}

**Descrizione:** Configura le opzioni SDK globali. Accetta un **Mappa\&lt;string string=&quot;&quot;>** come argomento. I valori della mappa verranno passati al server insieme a ogni chiamata di rete effettuata dall&#39;SDK.

I valori vengono passati al server indipendentemente dal flusso corrente (autenticazione/autorizzazione). Se desideri modificare i valori, puoi chiamare questo metodo in qualsiasi momento.

 

| Chiamata API: setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**Disponibilità:** v3.0+

**Parametri:**

- *opzioni*: Una mappa\&lt;string string=&quot;&quot;> contenente le opzioni SDK globali. Attualmente sono disponibili le seguenti opzioni:
   - **applicationProfile** : può essere utilizzato per creare configurazioni server basate su questo valore.
   - **ap\_vi** : ID visitatore del Marketing Cloud. Questo valore può essere utilizzato in seguito per i rapporti di analisi avanzata.
   - **device\_info** - Informazioni sul dispositivo come descritto in **Passaggio del manuale di informazioni sul dispositivo**

</br>

### checkAuthentication {#checkAuthN}

**Descrizione:** Controlla lo stato di autenticazione. A tale scopo, cerca un token di autenticazione valido nello spazio di archiviazione dei token locale. La chiamata a questo metodo non esegue chiamate di rete. Viene utilizzata dall’applicazione per eseguire una query sullo stato di autenticazione dell’utente e aggiornare di conseguenza l’interfaccia utente (ad esempio, aggiornare l’interfaccia utente di accesso/disconnessione). Lo stato di autenticazione viene comunicato all’applicazione tramite [*setAuthenticationStatus()*](#setAuthNStatus) callback.

Se un MVPD supporta la funzione &quot;Autenticazione per richiedente&quot;, è possibile memorizzare su un dispositivo più token di autenticazione. 

| Chiamata API: controlla lo stato di autenticazione |
| --- |
| ```public void checkAuthentication()``` |

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivati:** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**Descrizione:** Avvia il flusso di lavoro di autenticazione completo. Viene avviato controllando lo stato di autenticazione. Se non è già autenticato, viene avviato il computer dello stato del flusso di autenticazione:

- Se l&#39;ultimo tentativo di autenticazione ha avuto esito positivo, la fase di selezione MVPD viene ignorata e un controllo WebView presenta all&#39;utente la pagina di accesso di MVPD.
- Se l’ultimo tentativo di autenticazione non ha avuto esito positivo o se l’utente si è esplicitamente disconnesso, il [*displayProviderDialog()*](#displayProviderDialog) callback attivato. L&#39;applicazione utilizza questo callback per visualizzare l&#39;interfaccia utente di selezione MVPD. Inoltre, l’app deve riprendere il flusso di autenticazione informando la libreria di Access Enabler della selezione MVPD dell’utente tramite [setSelectedProvider()](#setSelectedProvider) metodo.

Se un MVPD supporta la funzione &quot;Autenticazione per richiedente&quot;, è possibile memorizzare su un dispositivo più token di autenticazione (uno per programmatore).

Infine, lo stato di autenticazione viene comunicato all’applicazione tramite *setAuthenticationStatus()* callback.

| Chiamata API: avvia il flusso di autenticazione |
| --- |
| ```public void getAuthentication()``` |

**Disponibilità:** v1.0+

| Chiamata API: avvia il flusso di autenticazione |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *forceAuthn*: flag che specifica se avviare il flusso di autenticazione, indipendentemente dal fatto che l’utente sia già autenticato o meno.
- *dati*: una mappa costituita da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l’SDK.

**Callback attivati:** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**Descrizione** Callback attivato da Access Enabler per informare l&#39;applicazione che è necessario creare un&#39;istanza degli elementi dell&#39;interfaccia utente appropriati per consentire all&#39;utente di selezionare l&#39;MVPD desiderato. Il callback fornisce un elenco di oggetti MVPD con informazioni aggiuntive che possono aiutare a creare correttamente il pannello dell&#39;interfaccia utente di selezione (come l&#39;URL che punta al logo MVPD, il nome visualizzato intuitivo, ecc.)

Dopo che l’utente ha selezionato l’MVPD desiderato, l’applicazione di livello superiore deve riprendere il flusso di autenticazione chiamando *setSelectedProvider()* e trasmettendogli l’ID del MVPD corrispondente alla selezione dell’utente.\
 

| **Callback: visualizzare l&#39;interfaccia utente di selezione MVPD** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**Disponibilità:** v1.0+

**Parametri**:

- *mvpds*: elenco di oggetti MVPD contenenti informazioni relative a MVPD che l’applicazione può utilizzare per creare gli elementi dell’interfaccia utente di selezione MVPD.

**Attivato da:** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**Descrizione:** Questo metodo viene richiamato dall&#39;applicazione per informare l&#39;Access Enabler della selezione MVPD dell&#39;utente. Quando si passa *nulle* come parametro, Access Enabler reimposta il MVPD corrente su un valore null.

| **Chiamata API: imposta il provider attualmente selezionato** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**Disponibilità:**v 1.0+

**Parametri:** Nessuno

**Callback attivati:** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navigateToUrl {#navigagteToUrl}

**Descrizione:** Callback attivato dall&#39;Access Enabler sull&#39;SDK per Android. Deve essere ignorato nell’SDK di Amazon FireOS.

| **Callback: visualizzazione della pagina di accesso MVPD** |
| --- |
| ```public void navigateToUrl(String url)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *url*: URL che punta alla pagina di accesso di MVPD

**Attivato da:** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**Descrizione:** Completa il flusso di autenticazione richiedendo il token di autenticazione dal server back-end. 

| **Chiamata API: recupera il token di autenticazione** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *cookie*: cookie impostati sul dominio di destinazione (consulta l’applicazione demo nell’SDK per un’implementazione di riferimento).

**Callback attivati:** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**Descrizione:** Callback attivato dall&#39;Access Enabler che informa l&#39;applicazione dello stato dell&#39;autenticazione. In molti casi il flusso di autenticazione può non riuscire, a causa dell’interazione dell’utente o di altri scenari imprevisti (ad esempio, problemi di connettività di rete, ecc.). Questo callback informa l’applicazione dello stato di esito positivo/negativo dell’autenticazione, fornendo al contempo informazioni aggiuntive sul motivo dell’errore, quando necessario.

Questo callback segnala anche quando il flusso di logout è completo.

| **Callback: segnala lo stato del flusso di autenticazione** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *stato*: può assumere uno dei seguenti valori:
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS` - flusso di autenticazione completato
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR` - flusso di autenticazione non riuscito
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT` - disconnessione
- *codice*: motivo dello stato presentato. Se *stato* è `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`, quindi *codice* è una stringa vuota (definita da `AccessEnabler.USER_AUTHENTICATED` costante). Se non è autenticato, questo parametro può assumere uno dei seguenti valori:
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR` : utente non autenticato. In risposta al *checkAuthentication()* chiamata al metodo quando non è presente alcun token di autenticazione valido nella cache dei token locale.
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler ha reimpostato il computer dello stato di autenticazione dopo il passaggio dell&#39;applicazione di livello superiore *nulle* a `setSelectedProvider()` per interrompere il flusso di autenticazione.  Presumibilmente l’utente ha annullato il flusso di autenticazione (ovvero ha premuto il pulsante &quot;Indietro&quot;).
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR` - Flusso di autenticazione non riuscito per motivi quali la non disponibilità della rete o l&#39;annullamento esplicito del flusso di autenticazione da parte dell&#39;utente.
   - `AccessEnabler.LOGOUT` : l&#39;utente non è stato autenticato a causa di un&#39;azione di disconnessione. 

**Attivato da:** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**Descrizione:** Questo metodo viene utilizzato dall’applicazione per determinare se l’utente è già autorizzato a visualizzare risorse protette specifiche. Lo scopo principale di questo metodo è quello di recuperare informazioni da utilizzare per decorare l’interfaccia utente (ad esempio, per indicare lo stato di accesso con le icone di blocco e sblocco).

| **Chiamata API: imposta il provider attualmente selezionato** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Disponibilità:** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> Il `resources` Il parametro è un array di risorse per cui deve essere controllata l&#39;autorizzazione.** Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID della risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa in `getAuthorization()` deve essere un valore concordato tra il programmatore e l’MVPD o un frammento RSS del contenuto multimediale.

**Callback attivato:** `preauthorizedResources()`

</br>

### risorse preautorizzate {#preauthResources}

**Descrizione:** Callback attivato da checkPreauthorizedResources(). Fornisce un elenco delle risorse che l’utente è già autorizzato a visualizzare.

| **Chiamata API: imposta il provider attualmente selezionato** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**Disponibilità:**v 1.0+

**Parametri:** Il `resources` Il parametro è un array di risorse per le quali l’utente è già autorizzato a visualizzare.

**Attivato da:** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per controllare lo stato di autorizzazione. Viene innanzitutto verificato lo stato di autenticazione. Se non autenticato, il *setTokenRequestFailed()* viene attivato il callback e il metodo viene chiuso. Se l’utente è autenticato, attiva anche il flusso di autorizzazione. Vedi i dettagli su *getAuthorization()* metodo.

| **Chiamata API: controlla lo stato di autorizzazione** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**Disponibilità:** v1.0+

| **Chiamata API: controlla lo stato di autorizzazione** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *resourceId*: ID della risorsa per la quale l’utente richiede l’autorizzazione.
- *dati*: una mappa costituita da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l’SDK.

**Callback attivati:** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**Descrizione:** Questo metodo viene utilizzato dall&#39;applicazione per avviare il flusso di autorizzazione. Se l’utente non è già autenticato, avvia anche il flusso di autenticazione. Se l’utente viene autenticato, Access Enabler procede con il rilascio di richieste per il token di autorizzazione (se non è presente alcun token di autorizzazione valido nella cache dei token locale) e per il token multimediale di breve durata. Una volta ottenuto il token multimediale breve, il flusso di autorizzazione viene considerato completo. Il *setToken()* il callback viene attivato e il token multimediale breve viene distribuito come parametro all’applicazione. Se, per qualsiasi motivo, l&#39;autorizzazione non riesce, il *tokenRequestFailed()* viene attivato il callback e vengono forniti il codice di errore e i dettagli.

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
- *dati*: una mappa costituita da coppie chiave-valore da inviare al servizio di pass Pay-TV. Adobe può utilizzare questi dati per abilitare funzionalità future senza modificare l’SDK. 

**Callback attivati:** `tokenRequestFailed(), setToken(), sendTrackingData()`

|  |  |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **Callback aggiuntivi attivati**  <br>Questo metodo può anche attivare i seguenti callback (se viene avviato anche il flusso di autenticazione): _setAuthenticationStatus()_, _displayProviderDialog()_ |

**NOTA: se possibile, utilizza checkAuthorization() invece di getAuthorization(). Il metodo getAuthorization() avvierà un flusso di autenticazione completo (se l’utente non è autenticato) e ciò potrebbe comportare una complicata implementazione da parte del programmatore.**

</br>

### setToken {#setToken}

**Descrizione:** Callback attivato da Access Enabler che informa l&#39;applicazione che il flusso di autorizzazione è stato completato correttamente. Anche il token multimediale di breve durata viene distribuito come parametro.

| **Callback: flusso di autorizzazione completato** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**Disponibilità:**v 1.0+

**Parametri:**

- *token*: token multimediale di breve durata
- *resourceId*: risorsa per la quale è stata ottenuta l’autorizzazione

**Attivato da:** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**Descrizione:** Callback attivato da Access Enabler che informa l&#39;applicazione di livello superiore che il flusso di autorizzazione non è riuscito.

| **Callback: flusso di autorizzazione non riuscito** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *resourceId*: risorsa per la quale è stata ottenuta l’autorizzazione
- *errorCode*: codice di errore associato allo scenario di errore. Valori possibili:
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR` - L&#39;utente non è stato in grado di autorizzare per la risorsa specificata
- *errorDescription*: ulteriori dettagli sullo scenario di errore. Se questa stringa descrittiva non è disponibile per alcun motivo, l’autenticazione Adobe Primetime invia una stringa vuota >**(&quot;&quot;)**.  Questa stringa può essere utilizzata da un MVPD per trasmettere messaggi di errore personalizzati o messaggi relativi alle vendite. Ad esempio, se a un abbonato viene negata l’autorizzazione per una risorsa, l’MVPD potrebbe inviare un messaggio del tipo: &quot;Attualmente non hai accesso a questo canale nel pacchetto. Se desideri aggiornare il pacchetto, fai clic qui.&quot; Il messaggio viene passato dall’autenticazione di Adobe Primetime tramite questo callback al programmatore, che ha la possibilità di visualizzarlo o ignorarlo. L’autenticazione Adobe Primetime può inoltre utilizzare questo parametro per fornire una notifica della condizione che potrebbe aver causato un errore. Ad esempio, &quot;Si è verificato un errore di rete durante la comunicazione con il servizio di autorizzazione del provider&quot;.

**Attivato da:** `checkAuthorization(), getAuthorization()`

</br>

### logout {#logout}

**Descrizione:** Utilizzare questo metodo per avviare il flusso di logout. La disconnessione è il risultato di una serie di operazioni di reindirizzamento HTTP dovute al fatto che l’utente deve essere disconnesso sia dai server di autenticazione di Adobe Primetime che dai server MVPD. 

| **Chiamata API: avvia il flusso di logout** |
| --- |
| ```public void logout()``` |

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivati:** Nessuno

</br>

### getSelectedProvider {#getSelectedProvider}

**Descrizione:** Utilizzare questo metodo per determinare il provider attualmente selezionato.

| **Chiamata API: determina il MVPD attualmente selezionato** |
| --- |
| ```public void getSelectedProvider()``` |

**Disponibilità:** v1.0+

**Parametri:** Nessuno

**Callback attivati:** `selectedProvider()`

</br>

### selectedProvider {#selectedProvider}

**Descrizione:** Callback attivato dall&#39;Access Enabler che fornisce all&#39;applicazione informazioni sull&#39;MVPD attualmente selezionato.

| **Callback: informazioni sull&#39;MVPD attualmente selezionato** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *mvpd*: oggetto contenente informazioni sull’MVPD attualmente selezionato

**Attivato da:** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**Descrizione:** Utilizzare questo metodo per recuperare informazioni esposte come metadati dalla libreria di Access Enabler. L&#39;applicazione può accedere a queste informazioni fornendo un oggetto MetadataKey composito.

| **Chiamata API: query di AccessEnabler per i metadati** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**Disponibilità:** v1.0+

Esistono due tipi di metadati disponibili per i programmatori:

- Metadati statici (TTL del token di autenticazione, TTL del token di autorizzazione e ID dispositivo) 
- Metadati utente (informazioni specifiche dell’utente, come ID utente e codice postale; trasmessi da un MVPD al dispositivo di un utente durante i flussi di autenticazione e/o autorizzazione)

**Parametri:**

- *metadataKey*: struttura di dati che incapsula una variabile chiave e args, con il seguente significato:
   - Se la chiave è `METADATA_KEY_TTL_AUTHN` viene quindi eseguita la query per ottenere la data di scadenza del token di autenticazione.
   - Se la chiave è `METADATA_KEY_TTL_AUTHZ` e contiene un oggetto SerializableNameValuePair con nome = `METADATA_ARG_RESOURCE_ID` e valore = `[resource_id]`, quindi viene eseguita la query per ottenere la scadenza del token di autorizzazione associato alla risorsa specificata.
   - Se la chiave è `METADATA_KEY_DEVICE_ID` quindi viene eseguita la query per ottenere l’id dispositivo corrente. Tieni presente che questa funzione è disabilitata per impostazione predefinita e i programmatori devono contattare l’Adobe per informazioni sull’abilitazione e sulle tariffe.
   - Se la chiave è `METADATA_KEY_USER_META` e contiene un oggetto SerializableNameValuePair con nome = `METADATA_KEY_USER_META` e valore = `[metadata_name]`, quindi viene eseguita la query per i metadati dell’utente. L’elenco corrente dei tipi di metadati utente disponibili:
      - `zip` - CAP
      - `householdID` - Identificatore della famiglia. Se un MVPD non supporta i conti secondari, questo sarà identico a `userID`.
      - `maxRating` - Classificazione genitoriale massima per l&#39;utente
      - `userID` : identificatore utente. Se un MVPD supporta gli account secondari e l&#39;utente non è l&#39;account principale,
      - `channelID` - Un elenco di canali che l’utente ha il diritto di visualizzare

I metadati utente effettivi disponibili per un programmatore dipendono da ciò che viene reso disponibile da un MVPD.  Questo elenco verrà ulteriormente esteso man mano che nuovi metadati saranno disponibili e aggiunti al sistema di autenticazione di Adobe Primetime.

**Callback attivati:** [`setMetadataStatus()`](#setMetadaStatus)

**Ulteriori informazioni:** [Metadati utente](#setmetadatastatus)

</br>

### setMetadataStatus {#setMetadaStatus}

**Descrizione:** Callback attivato dall&#39;Access Enabler che distribuisce i metadati richiesti tramite un *getMetadata()* chiamare.

| **Callback: risultato della richiesta di recupero dei metadati** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**Disponibilità:** v1.0+

**Parametri:**

- *chiave*: oggetto MetadataKey contenente la chiave per la quale viene richiesto il valore dei metadati e i parametri associati (consulta applicazione demo per un’implementazione di riferimento).
- *risultato*: oggetto composito contenente i metadati richiesti. L’oggetto dispone dei seguenti campi:
   - *simpleResult*: elemento String che rappresenta il valore dei metadati quando è stata effettuata la richiesta per il valore TTL di autenticazione, TTL di autorizzazione o ID dispositivo. Questo valore è nullo se la richiesta è stata effettuata per i metadati utente.

   - *userMetadataResult*: un oggetto che contiene la rappresentazione Java di un payload di metadati utente JSON. Ad esempio:

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
 

Questo valore è nullo quando la richiesta è stata effettuata per metadati semplici (TTL di autenticazione, TTL di autorizzazione o ID dispositivo).

- *crittografato*: valore booleano che specifica se i metadati recuperati sono crittografati o meno. Questo parametro è significativo solo per le richieste di metadati utente, non ha significato per i metadati statici (ad esempio, TTL di autenticazione) che vengono sempre ricevuti non crittografati. Se questo parametro è impostato su True, spetta al programmatore ottenere il valore dei metadati utente non crittografati eseguendo una decrittografia RSA utilizzando la chiave privata dell&#39;inserimento nella whitelist (la stessa chiave privata utilizzata per la firma dell&#39;ID richiedente nella [`setRequestor`](#setRequestor) chiamata).

**Attivato da:** [`getMetadata()`](#getMetadata)

**Ulteriori informazioni:** [Metadati utente](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**Descrizione:** Utilizzare questo metodo per recuperare la versione corrente di AccessEnabler  

| **Chiamata API: ottieni versione di AccessEnabler** |
| --- |
| ```public static String getVersion()``` |

## Tracciamento degli eventi {#tracking}

L’Access Enabler attiva un callback aggiuntivo che non è necessariamente correlato ai flussi di adesione. Implementazione della funzione di callback di tracciamento degli eventi denominata *sendTrackingData()* è facoltativo, ma consente all’applicazione di tenere traccia di eventi specifici e di compilare statistiche quali il numero di tentativi di autenticazione/autorizzazione riusciti/non riusciti. Di seguito è riportata la specifica per *sendTrackingData()* callback:

### sendTrackingData {#sendTrackingData}

**Descrizione:** Callback attivato dall&#39;Access Enabler che segnala all&#39;applicazione il verificarsi di vari eventi come il completamento/il fallimento dei flussi di autenticazione/autorizzazione. Il tipo di dispositivo, il tipo di client Access Enabler e il sistema operativo vengono inoltre segnalati da sendTrackingData().

>[!WARNING]
>
> Il tipo di dispositivo e il sistema operativo sono derivati dall’utilizzo di una libreria Java pubblica (http://java.net/projects/user-agent-utils) e della stringa dell’agente utente. Tieni presente che queste informazioni vengono fornite solo come metodo grezzo per suddividere le metriche operative in categorie di dispositivi, ma che l’Adobe non può assumersi alcuna responsabilità per risultati errati. Utilizza la nuova funzionalità di conseguenza.

- Valori possibili per il tipo di dispositivo:
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- Valori possibili per il tipo di client Access Enabler:
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

- *evento*: l’evento di cui viene tenuto traccia. Esistono tre possibili tipi di eventi di tracciamento:
   - **authorizationDetection:** ogni volta che viene restituita una richiesta di token di autorizzazione (il tipo di evento è `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection:** ogni volta che si verifica un controllo di autenticazione (il tipo di evento è `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** quando l’utente seleziona un MVPD nel modulo di selezione MVPD (il tipo di evento è `EVENT_MVPD_SELECTION`)
- *dati*: dati aggiuntivi associati all’evento segnalato. Questi dati vengono presentati sotto forma di elenco di valori.

Di seguito sono riportate le istruzioni per l’interpretazione dei valori in *dati* array:

- Per tipo di evento *`EVENT_AUTHN_DETECTION`:*
   - **0** - Indica se la richiesta del token è riuscita (true/false) e se quanto sopra è vero:
   - **1** - Stringa ID MVPD
   - **2** - GUID (hash MD5)
   - **3** - Token già nella cache (true/false)
   - **4** - Tipo di dispositivo
   - **5** - Tipo di client Access Enabler
   - **6** - Tipo di sistema operativo

- Per tipo di evento `EVENT_AUTHZ_DETECTION`
   - **0** - Se la richiesta del token è stata eseguita correttamente (true/false) e in caso di esito positivo:
   - **1** - ID MVPD
   - **2** - GUID (hash MD5)
   - **3** - Token già nella cache (true/false)
   - **4** - Errore
   - **5** - Dettagli
   - **6** - Tipo di dispositivo
   - **7** - Tipo di client Access Enabler
   - **8** - Tipo di sistema operativo

- Per tipo di evento `EVENT_MVPD_SELECTION`
   - **0** - ID del MVPD attualmente selezionato
   - **1** - Tipo di dispositivo
   - **2** - Tipo di client Access Enabler
   - **3** - Tipo di sistema operativo

**Attivato da:** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
