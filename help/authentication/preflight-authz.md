---
title: Autorizzazione di verifica preliminare
description: Autorizzazione di verifica preliminare
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---



# Autorizzazione di verifica preliminare {#preflight-authorization}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Panoramica {#overview}

Questa funzione fornisce un controllo di autorizzazione leggero per più risorse. Lo scopo di questo controllo leggero è decorare l’interfaccia utente (ad esempio, per indicare lo stato di accesso con le icone di blocco e sblocco). L’autorizzazione di verifica preliminare è il più leggera ed efficiente possibile, in modo tale che una singola chiamata API generi lo stato di autorizzazione per un elenco di risorse. Questa funzione non è autorevole per quanto riguarda l’autorizzazione di una risorsa.

A `getAuthorization(resource)` o `checkAuthorization(resource)` deve essere effettuata una chiamata ancora prima di consentire la riproduzione.

L’autorizzazione Preflight fornisce inoltre il supporto per un caso d’uso diverso, in cui il programmatore deve richiedere l’autorizzazione per più ID di risorse per consentire la riproduzione di un elemento del contenuto multimediale. Il programmatore può eseguire un controllo preliminare iniziale sulle risorse richieste e, a seconda della risposta, potrebbe fallire presto se le condizioni aziendali non sono soddisfatte.

Per un elenco degli MVPD che supportano l&#39;autorizzazione di preflight, vedere [Autorizzazione di verifica preliminare MVPD](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) pagina. 

>[!NOTE]
>
> Tieni presente che l’utilizzo di questa funzione per gli MVPD che non dispongono del supporto completo per l’autorizzazione di preflight deve essere concordato in anticipo con gli Adobi e gli MVPD. L&#39;uso dell&#39;autorizzazione di preflight su questi MVPD cadrà nello &quot;scenario peggiore&quot; descritto [qui](/help/authentication/mvpd-preflight-authz.md#intro) e può causare problemi di prestazioni e tempi di risposta lenti. </br>
> Inoltre, si prega di notare che l&#39;uso dell&#39;autorizzazione di preflight con **più di 5 risorse devono essere esplicitamente concordate dall&#39;Adobe**.

## API di preflight di AccessEnabler {#AE_pre_api}

AccessEnabler espone una coppia di funzioni API/callback per implementare l&#39;autorizzazione di preflight. La chiamata API richiede un singolo parametro composto da un elenco di risorse. La funzione di callback richiede un singolo parametro che rappresenta le risorse autorizzate effettive. Gli esempi seguenti sono in ActionScript, ma le chiamate sono disponibili in tutte le versioni di AccessEnabler.

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

Chiama questa funzione sull&#39;oggetto AccessEnabler per richiedere lo stato di autorizzazione per un elenco di risorse.

Il parametro resources è l’elenco delle risorse per le quali è necessario controllare l’autorizzazione. Ogni elemento dell’elenco deve essere una stringa che rappresenta l’ID risorsa. L’ID risorsa è soggetto alle stesse limitazioni dell’ID risorsa nel `getAuthorization()` chiama, cioè, è concordato sul valore stabilito tra il programmatore e il MVPD, o un frammento RSS media. Tieni presente che l’autenticazione Adobe Primetime non gestisce le risorse in alcun modo, ad eccezione di un livello di mediazione sottile che può trasformare i formati delle risorse in base a ciò che l’MVPD supporta effettivamente.

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

Questa è una funzione di callback che deve essere implementata nell&#39;applicazione a livello superiore del programmatore. AccessEnabler chiamerà questa funzione dopo aver calcolato l&#39;elenco delle risorse autorizzate.


### Esempio JS

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## Informazioni di implementazione {#details}

- [Preflight Using ChannelID](#preflight_using_channelID)
- [POST / Preautorizzare](#post)
- [Storage](#storage)

La chiamata API cerca di trovare un elenco memorizzato nella cache delle risorse autorizzate per l’utente corrente nell’archivio locale del client. Se non è presente alcun elenco memorizzato nella cache, viene effettuata una chiamata HTTPS ai server AdobePass per recuperare l’elenco.

Il meccanismo di caching migliora i tempi di prestazioni nelle chiamate successive saltando completamente la chiamata di rete. Inoltre, l’elenco memorizzato in cache può essere compilato in anticipo come parte del processo di autenticazione.  (Per informazioni sulla configurazione di questo scenario, vedi [Integrazione dell&#39;autorizzazione di preflight](/help/authentication/authz-usecase.md#preflight_authz_int) nella sezione Autorizzazione della Guida all&#39;integrazione MVPD).

Inoltre, l’elenco delle risorse memorizzate nella cache può potenzialmente essere utilizzato per ottimizzare il flusso di autorizzazione, nel senso che se esiste un elenco di risorse nella cache, `checkAuthorization()` può controllare prima di effettuare una chiamata di rete. Se la risorsa non è presente nell’elenco delle risorse preautorizzate, il controllo può non riuscire senza dover chiamare i server di autenticazione Primetime.


### Preflight Using ChannelID {#preflight_using_channelID}

A partire dalla versione 2.4.1 di Primetime Authentication, il flusso di Preflight funziona come segue:

1. Durante l&#39;autenticazione, l&#39;autenticazione Primetime legge il `channelIID` dalla risposta SAML dell&#39;MVPD e utilizza questo valore per impostare l&#39; `authorizedResources` nel token di autenticazione.
1. Dentro `checkPreauthorizedResources()` Funzione API, autenticazione Primetime controlla se `authorizedResources` è impostato.
1. Se la `authorizedResources` è impostato, l’autenticazione di Primetime legge tale valore ed esegue un’intersezione tra l’elenco delle risorse e `authorizedResources` e l&#39;elenco delle risorse ricevute da `checkPreauthorizedResources()` parametro .  Il risultato di questa intersezione è l&#39;elenco finale delle risorse preautorizzate.
1. Se la `authorizedResources` non è impostato, esegui il flusso implementato in precedenza, in cui l’elenco delle risorse ricevute da `checkPreauthorizedResources()` viene passato al PreAuthorizationServlet. Questo servlet esegue le chiamate di autorizzazione agli endpoint MVPD e restituisce l&#39;elenco delle risorse preautorizzate.

### Esempio di verifica preliminare con ChannelID

L’esempio seguente mostra un esempio di line-up di canali. Il nome dell&#39;attributo utilizzato per inviare l&#39;elenco dei canali può essere diverso da un MVPD a un altro:

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

La `authorizedResources` l’elemento dell’elemento di autenticazione viene visualizzato come segue:

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

Il programmatore esegue il `checkPreauthorizedResources()` Chiamata API, passando il seguente elenco di parametri:</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

L’implementazione di Preflight corrente esegue l’intersezione con l’elenco di risorse della `authorizedResources` e restituisce questo elenco:

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**Nota:** Si prega di notare che l&#39;intersezione non distingue tra maiuscole e minuscole.

 

### POST / Preautorizzare {#post}

Questa chiamata viene eseguita automaticamente da AccessEnabler quando non esiste un elenco di risorse nella cache e autorizzato. 


#### Richiesta {#req}

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `authentication_token` | string | SÌ | Token di autenticazione. |
| `resource_id` | string | SÌ | Una singola risorsa. Può essere specificato più volte, una volta per ogni elemento della matrice delle risorse fornita nel `checkPreauthorizedResources()` Chiamata API. |


**Nota:** È possibile configurare il numero massimo di risorse richieste.
**Il valore predefinito massimo è 5.**


#### Risposta {#resp}

La risposta inviata nuovamente dal servlet di preautorizzazione ha il seguente formato:

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### Storage {#storage}

Elenco delle risorse preautorizzate che AccessEnabler ottiene dal provider di servizi. Elenco delle risorse:

- È memorizzato insieme ai token AuthN e AuthZ
- È valido purché l’utente si trovi sullo stesso sito web o fino alla scadenza del token AuthN
- Viene recuperato ogni volta che l’utente arriva a un nuovo sito web integrato di autenticazione Primetime

Ogni voce contiene l’ID risorsa per il quale l’utente è preautorizzato.

Ad esempio:


| ID risorsa | Autorizzato |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


Questo elenco è denominato &quot;cache di preautorizzazione&quot;.

#### Flusso {#flow}

1. L&#39;app / sito del programmatore crea un `checkPreauthorizedResources(resourceList)` chiama.
1. AccessEnabler verifica il token di autenticazione per le risorse autorizzate:
   1. Se il token di autenticazione contiene risorse autorizzate - questo elenco è autorevole e non deve essere effettuata alcuna chiamata per ottenere queste informazioni. La ricerca delle risorse di resourceList si trova nell&#39;elenco delle risorse autorizzate nel token di autenticazione e solo quelle trovate vengono restituite dal `preauthorizedResources()` callback.
   1. Se il token di autenticazione NON CONTIENE risorse autorizzate - `resourceList` viene confrontato con l’elenco di risorse nella cache di preautorizzazione.
      1. Se l’elenco contiene le stesse risorse, significa che è già stata effettuata una chiamata al server e che la risposta è già presente nella cache di preautorizzazione. Solo le risorse autorizzate verranno restituite dalla `preauthorizedResources()` callback.
      1. Se l&#39;elenco NON contiene le stesse risorse, il client deve effettuare una chiamata al server per ottenere lo stato di autorizzazione per le risorse in resourceList. La risposta verrà recuperata e memorizzata nella cache di preautorizzazione, sostituendo completamente le vecchie risorse. Solo le risorse autorizzate verranno restituite dalla `preauthorizedResources()` callback.


#### Recupero elenco {#listRetrieve}

Ogni volta che un `checkPreauthorizedResources()` viene chiamato , l’elenco delle risorse per verificare l’autorizzazione viene controllato nella cache di preautorizzazione. Se l’elenco contiene lo stesso set di risorse, non viene effettuata alcuna chiamata al provider di servizi, in quanto tutte le risorse necessarie per attivare il `preauthorizedResources()` callback già presenti nella cache.


#### logout() {#logout}

La cache di preautorizzazione viene svuotata al momento dell’uscita.


## Dipendenze {#depends}

Le prestazioni dell’API Preflight dipendono da implementazioni MVPD specifiche.  Per le opzioni di implementazione, consulta [Integrazione dell&#39;autorizzazione di preflight](/help/authentication/authz-usecase.md#preflight_authz_int) nella sezione Autorizzazione della Guida all&#39;integrazione MVPD.


## Sicurezza {#security}

Le API client sono disponibili per tutti i programmatori.

L&#39;implementazione utilizza HTTPS come mezzo di trasporto, ma per poter effettuare una chiamata più leggera non vengono utilizzate misure di sicurezza aggiuntive (nessuna firma, nessun FAXS).

**Attenzione:** NON utilizzare questa API in modo autorevole per determinare se a un utente deve essere concesso l&#39;accesso a una risorsa protetta. Lo scopo di questa API è la decorazione dell’interfaccia utente e/o la verifica preliminare delle decisioni aziendali. La `getAuthorization()` e `checkAuthorization()` le chiamate devono sempre essere effettuate prima di consentire la riproduzione.


## Compatibilità {#compat}

Questa funzione è supportata in tutte le versioni di AccessEnabler: AS, JS, AIR, iOS, Android, Xbox (nel flusso AuthN a 2 schermi).

L’autorizzazione di verifica preliminare non supporta le risorse di preautorizzazione contenenti sezioni CDATA. L&#39;obiettivo del sistema di verifica preliminare corrente è quello di supportare il filtraggio a livello di canale. Le risorse con sezioni CDATA sono probabilmente risorse a livello di risorsa. Preflight supporta la semplicità `mrss` risorse per la pre-autorizzazione a livello di canale, purché non contengano CDATA. 

## Integrazione Con Altre Funzionalità {#integ_w_other_features}

Una possibile ottimizzazione può verificarsi sul flusso di autorizzazione per generare un errore veloce se la risorsa non è nell’elenco delle risorse preautorizzate.

In questa ottimizzazione, l’endpoint di preflight del server si integra con il meccanismo di degradazione.  

Se per MVPD e Requestor è in vigore una regola &quot;AuthN All&quot;, l&#39;endpoint di verifica preliminare eseguirà semplicemente il mirroring di tutte le risorse ricevute nella richiesta.

Lo stesso vale se &quot;AuthZ All&quot; è abilitato per almeno una delle risorse presenti nella richiesta.

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
