---
title: Autorizzare
description: Autorizzazione preventiva di JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# Autorizzare {#js-preauthorize}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#preauth-overview}

Il metodo API di preautorizzazione deve essere utilizzato dalle applicazioni per ottenere decisioni di preautorizzazione per una o più risorse. La richiesta API di preautorizzazione deve essere utilizzata per i suggerimenti dell’interfaccia utente e/o per il filtraggio dei contenuti. Prima di consentire l’accesso dell’utente alle risorse specificate, è necessario effettuare una richiesta API di autorizzazione effettiva.

Nel caso in cui si verifichi un errore imprevisto (ad esempio, un problema di rete e l&#39;endpoint di autorizzazione MVPD non disponibile) quando una richiesta API di autorizzazione preventiva viene elaborata dai servizi di autenticazione di Adobe Primetime, verranno incluse una o più informazioni di errore separate per le risorse interessate come parte del risultato della risposta di autorizzazione API di preautorizzazione.

### preautorizzazione pubblica(richiesta: PreautorizzareRequest, callback: AccessEnablerCallback&lt;any>): void {#preauth-method}

**Descrizione:** Questo metodo deve essere utilizzato dalle applicazioni per ottenere le decisioni di preautorizzazione (informative) degli utenti autenticati dal servizio di autenticazione di Adobe Primetime per visualizzare risorse protette specifiche, allo scopo principale di decorare l&#39;interfaccia utente dell&#39;applicazione (ad esempio, l&#39;indicazione dello stato di accesso con icone di blocco e sblocco).

**Disponibilità:** v4.4.0+

**Parametri:**

* `PreauthorizeRequest`: Oggetto Builder utilizzato per definire la richiesta
* `AccessEnablerCallback`: callback utilizzato per restituire la risposta API
* `PreauthorizeResponse`: Oggetto utilizzato per restituire il contenuto della risposta API

### Classe PreauthorizeRequestBuilder {#preath-req-builder-class}

#### setResources(resources: string[]): PreautorizzareRequestBuilder {#set-res-preath-req-buildr}

* Imposta l’elenco delle risorse per le quali desideri ottenere decisioni di preautorizzazione.
* È obbligatorio impostarlo per l’utilizzo dell’API di preautorizzazione.
* Ogni elemento dell&#39;elenco deve essere un elemento String che rappresenta il valore ID risorsa o il frammento RSS multimediale che deve essere concordato con l&#39;MVPD.
* Questo metodo imposta le informazioni solo nel contesto della `PreauthorizeRequestBuilder` istanza dell&#39;oggetto, che è il ricevitore di questa chiamata del metodo.

* Per creare un `PreauthorizeRequest` potete dare un&#39;occhiata `PreauthorizeRequestBuilder`metodo s:

```JavaScript
  build(): PreauthorizeRequest
```

* `@param {string[]}` risorse. Elenco delle risorse per le quali si desidera ottenere le decisioni di preautorizzazione.
* `@returns {PreauthorizeRequestBuilder}` Riferimento allo stesso `PreauthorizeRequestBuilder` istanza dell&#39;oggetto , che è il ricevitore della chiamata del metodo .
* Questo consente la creazione di concatenamento di metodi.

#### disableFeatures(...caratteristiche: string[]): PreautorizzareRequestBuilder {#disabl-featres-preauth-req-buildr}

* Imposta le funzionalità che desideri disattivarle quando ottieni decisioni di preautorizzazione.
* Questa funzione imposta le informazioni solo nel contesto della `PreauthorizeRequestBuilder` istanza dell&#39;oggetto, che è il ricevitore di questa chiamata della funzione.
* Per creare un `PreauthorizeRequest` potete dare un&#39;occhiata `PreauthorizeRequestBuilder`Funzione:

```JavaScript
public func build() -> PreauthorizeRequest
```

* `@param {string[]}` funzionalità. Set di funzioni che si desidera che siano disattivate.
* `@returns` Riferimento allo stesso `PreauthorizeRequestBuilder` istanza dell&#39;oggetto, che è il ricevitore della chiamata della funzione.
* Lo fa per consentire la creazione di una catena di funzioni.

#### build(): PreautorizzareRequest {#preauth-req}

* Crea e recupera il riferimento di un nuovo `PreauthorizeRequest` istanza oggetto.
* Questo metodo crea un&#39;istanza nuova `PreauthorizeRequest` ogni volta che viene chiamato.
* Questo metodo utilizza i valori impostati in anticipo nel contesto della `PreauthorizeRequestBuilder` istanza dell&#39;oggetto, che è il ricevitore di questa chiamata del metodo.
* Tenete presente che questo metodo non produce effetti collaterali,
* pertanto non altera lo stato dell&#39;SDK o lo stato del `PreauthorizeRequestBuilder` istanza dell&#39;oggetto, che è il ricevitore di questa chiamata del metodo.
* Ciò significa che le chiamate successive di questo metodo per lo stesso ricevitore creeranno nuove diverse `PreauthorizeRequest` istanze dell&#39;oggetto, ma con le stesse informazioni, nel caso in cui i valori siano impostati su `PreauthorizeRequestBuilder` se non sono state modificate tra le chiamate.
* Nel caso in cui non sia necessario aggiornare alcuna delle informazioni fornite (risorse e memorizzazione in cache), è possibile riutilizzare l’istanza PreauthorizeRequest per più utilizzi dell’API di preautorizzazione.
* `@returns {PreauthorizeRequest}`

### interfaccia AccessEnablerCallback&lt;t> {#interface-access-enablr-callback}

#### onResponse(result: T); {#on-response-result}

* callback di risposta chiamato dall&#39;SDK quando la richiesta API di preautorizzazione è stata soddisfatta.
* Il risultato è un esito positivo o un errore contenente uno stato.
* `@param {T} result`

#### onFailure(result: T); {#on-failure-result}

* Callback di errore chiamato dall&#39;SDK quando non è stato possibile soddisfare la richiesta API di preautorizzazione.
* Il risultato è un risultato di errore contenente uno stato.
* `@param {T} result`

### classe PreautorizzazioneResponse {#preauth-response-class}

#### status pubblico: Status; {#public-status}

* Restituisce: Informazioni aggiuntive sullo stato (stato) in caso di errore.
* Potrebbe tenere un `null` valore.

#### decisioni pubbliche: Decisione[]; {#public-decisions}

* Restituisce: L&#39;elenco delle decisioni di autorizzazione preventiva. Una decisione per ogni risorsa.
* L&#39;elenco potrebbe essere vuoto in caso di errore.

### stato classe {#class-status}

#### status pubblico: numero; {#public-status-numbr}

* Il codice di stato della risposta HTTP come documentato nella RFC 7231.
* Può essere 0 nel caso in cui il valore `Status` proviene dall’SDK invece dei servizi di autenticazione di Adobe Primetime.

#### codice pubblico: numero; {#public-code-numbr}

* Codice di errore standard dei servizi di autenticazione di Adobe Primetime.
* Potrebbe contenere una stringa vuota o una `null` valore.

#### messaggio pubblico: stringa; {#public-msg-string}

* Messaggio dettagliato che in alcuni casi è fornito dagli endpoint di autorizzazione MVPD o dalle regole di degrado del programmatore.
* Potrebbe contenere una stringa vuota o una `null` valore.

#### dettagli pubblici: stringa; {#public-details-strng}

* Contiene un messaggio dettagliato che in alcuni casi è fornito dagli endpoint di autorizzazione MVPD o dalle regole di degradazione del programmatore.
* Potrebbe contenere una stringa vuota o una `null` valore.


#### public helpUrl: stringa; {#public-help-url-string}

* L’URL che effettua un collegamento a ulteriori informazioni sul motivo per cui si è verificato questo stato/errore e sulle possibili soluzioni.
* Potrebbe contenere una stringa vuota o una `null` valore.

#### traccia pubblica: stringa; {#public-trace-string}

* Identificatore univoco per questa risposta, che può essere utilizzato quando contatti il supporto per identificare problemi specifici in scenari più complessi.
* Potrebbe contenere una stringa vuota o una `null` valore.

#### azione pubblica: stringa; {#public-action-string}

* L&#39;azione raccomandata per rimediare alla situazione.
   * **nessuno**: Purtroppo non esiste un&#39;azione predefinita per risolvere questo problema. Questo potrebbe indicare una chiamata non corretta dell&#39;API pubblica
   * **configurazione**: È necessaria una modifica alla configurazione tramite il dashboard TVE o contattando il supporto.
   * **registrazione della domanda**: La domanda deve registrarsi nuovamente.
   * **autenticazione**: L&#39;utente deve eseguire l&#39;autenticazione o la riautenticazione.
   * **autorizzazione**: L’utente deve ottenere l’autorizzazione per la risorsa specifica.
   * **degradazione**: Si deve applicare una qualche forma di degradazione.
   * **riprovare**: Il nuovo tentativo di richiesta potrebbe risolvere il problema
   * **riprovare**: Se si ripete la richiesta dopo il periodo di tempo indicato, il problema potrebbe essere risolto.
* Potrebbe contenere una stringa vuota o una `null` valore.

### decisione di classe {#class-decision}

#### id pubblico: stringa; {#public-id-string}

* ID risorsa per cui è stata ottenuta la decisione.

#### pubblico autorizzato: booleano; {#public-auth-boolean}

* Il valore del flag che indica se la decisione ha esito positivo o meno.

#### errore pubblico: Status; {#public-error-status}

* Informazioni aggiuntive sullo stato (stato) in caso di errore. Potrebbe tenere un `null` valore.

## Esempio di implementazione client {#client-imp-example}

```JavaScript
let accessEnablerApi = new window.AccessEnabler.AccessEnabler("software statement");
let accessEnablerModels = window.AccessEnabler.models;



// Build request
let requestBuilder = new accessEnablerModels.PreauthorizeRequest.getBuilder();
let request = requestBuilder
    .setResources(["RES01", "RES02", "RES03"])
    .disableFeatures("LOCAL_CACHE")
    .build();



// Create callback
let callback = {
    onResponse(response) {
        // Handle onResponse
    },
    onFailure(response) {
        // Handle onFailure
    }
};

// Invoke call
accessEnablerApi.preauthorize(request, callback);
```


## Esempi di scenario {#scenario-examples}

### Scenario 1: Tutte le risorse richieste sono state autorizzate {#all-req-res-auth}

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Disabilitato</td>
    <td>

```JavaScript
        {
    "decisions": [
        {
        "id": "RES01",
        "authorized": true
        },
        {
        "id": "RES02",
        "authorized": true
        },
        {
        "id": "RES03",
        "authorized": true
        }
    ]
    }    
```

</td>
  </tr>
</tbody>


### Scenario 2: Alcune risorse richieste sono state autorizzate. {#sm-req-res-auth}

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Disabilitato</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;Decisioni&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizzato&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizzato&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizzato&quot;: true
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>Abilitato</td>
    <td>

    &quot;JavaScript
    {
    &quot;Decisioni&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizzato&quot;: true
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizzato&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_deny_by_mvpd&quot;,
    &quot;message&quot;: &quot;L&#39;MVPD ha restituito una decisione \&quot;Rifiuta\&quot; quando si richiede una pre-autorizzazione per la risorsa specificata.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizzato&quot;: true
    },
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Scenario 3: Nessuna delle risorse richieste è stata autorizzata. {#none-req-res-auth}

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
<tr>
    <td>Disabilitato</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;Decisioni&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizzato&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizzato&quot;: false
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizzato&quot;: false
    }
    ]
    }
    
    &quot;

</td>
  </tr>

<tr>
    <td>Abilitato</td>
    <td>

    &quot;JavaScript
    
    {
    &quot;Decisioni&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizzato&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_deny_by_mvpd&quot;,
    &quot;message&quot;: &quot;L&#39;MVPD ha restituito una decisione \&quot;Rifiuta\&quot; quando si richiede una pre-autorizzazione per la risorsa specificata.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizzato&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;preauthorization_deny_by_mvpd&quot;,
    &quot;message&quot;: &quot;L&#39;MVPD ha restituito una decisione \&quot;Rifiuta\&quot; quando si richiede una pre-autorizzazione per la risorsa specificata.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES03&quot;,
    &quot;autorizzato&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;maximum_execute_time_superamento&quot;,
    &quot;message&quot;: &quot;La richiesta non è stata completata nel tempo massimo consentito. Il nuovo tentativo della richiesta potrebbe risolvere il problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;riprovare&quot;
    }
    }
    ]
    }
    
    &quot;

</td>
  </tr>
</tbody>


### Scenario 4: Richiesta client non valida. Nessuna risorsa specificata. {#bad-cl-req-no-res-sp}

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Disabilitato/Abilitato</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 400,
    &quot;code&quot;: &quot;internal_error&quot;,
    &quot;message&quot;: &quot;Richiesta non riuscita a causa di un errore interno.&quot;,
    &quot;particolari&quot;: &quot;Il parametro String[] obbligatorio &#39;resource&#39; non è presente&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    },
    &quot;Decisioni&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Scenario 5: Richiesta client non valida. Sono state specificate risorse vuote. {#bad-cl-req-empt-res-sp}

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Disabilitato/Abilitato</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 412,
    &quot;code&quot;: &quot;missing_resource&quot;,
    &quot;message&quot;: &quot;Il parametro della risorsa è mancante&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;none&quot;
    },
    &quot;Decisioni&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Scenario 6: Errore di rete. {#ntwrk-error}

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Abilitato</td>
    <td>

    &quot;JavaScript
    {
    &quot;Decisioni&quot;: [
    {
    &quot;id&quot;: &quot;RES01&quot;,
    &quot;autorizzato&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_receive_error&quot;,
    &quot;message&quot;: &quot;Errore di lettura durante il recupero della risposta dal servizio partner associato. Il nuovo tentativo della richiesta potrebbe risolvere il problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;riprovare&quot;
    }
    },
    {
    &quot;id&quot;: &quot;RES02&quot;,
    &quot;autorizzato&quot;: false,
    &quot;error&quot;: {
    &quot;status&quot;: 403,
    &quot;code&quot;: &quot;network_receive_error&quot;,
    &quot;message&quot;: &quot;Errore di lettura durante il recupero della risposta dal servizio partner associato. Il nuovo tentativo della richiesta potrebbe risolvere il problema.&quot;,
    &quot;helpUrl&quot;: &quot;https://experienceleague.adobe.com/docs/primetime/authentication/home.html&quot;,
    &quot;action&quot;: &quot;riprovare&quot;
    }
    }
    ]
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

### Scenario 7: Il flusso di preautorizzazione è stato richiamato senza una sessione AuthN valida.

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Disabilitato/Abilitato</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;authentication_session_missing&quot;,
    &quot;message&quot;: &quot;Impossibile recuperare la sessione di autenticazione associata a questa richiesta. Per continuare, l&#39;utente deve effettuare nuovamente l&#39;autenticazione con un MVPD supportato.&quot;,
    &quot;action&quot;: &quot;authentication&quot;
    },
    &quot;Decisioni&quot;: []
    }
    
    &quot;

</td>
  </tr>
</tbody>
</table>



### Scenario 8: Il flusso di preautorizzazione è stato richiamato prima del completamento della chiamata setRequestor

<table>
<thead>
  <tr>
    <th>Flag di codice di errore avanzato</th>
    <th>Risposta</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Disabilitato/Abilitato</td>
    <td>

    &quot;JavaScript
    {
    &quot;status&quot;: {
    &quot;status&quot;: 0,
    &quot;code&quot;: &quot;requestor_not_configure&quot;,
    &quot;message&quot;: &quot;Il richiedente non è ancora configurato, il che costituisce un prerequisito per l’utilizzo di qualsiasi API oltre all’API setRequestor.&quot;,
    &quot;action&quot;: &quot;riprovare&quot;
    },
    &quot;Decisioni&quot;: []
    }
    &quot;

</td>
  </tr>
</tbody>
</table>

