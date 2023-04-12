---
title: Panoramica tecnica di Amazon FireOS
description: Panoramica tecnica di Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---


# Panoramica tecnica di Amazon FireOS {#amazon-fireos-technical-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

## Introduzione {#intro}

Amazon FireOS AccessEnabler è rappresentato da due componenti : una libreria stub AccessEnabler utilizzata dall&#39;applicazione e una libreria Java Android a livello di sistema che consente alle app mobili di utilizzare l&#39;autenticazione Adobe Primetime per i servizi di adesione di TV Everywhere. Un&#39;implementazione Android per Amazon FireOS è costituita dall&#39;interfaccia AccessEnabler che definisce l&#39;API di adesione e da un protocollo EntitlementDelegate che descrive i callback attivati dalla libreria. La libreria Android AccessEnabler a livello di sistema consente l&#39;accesso ai servizi Amazon per abilitare Single Sing On a livello di piattaforma.

## Informazioni sui flussi di lavoro dei client nativi {#native_client_workflows}

I flussi di lavoro client nativi sono generalmente uguali o molto simili a quelli dei client di autenticazione Primetime basati su browser. Tuttavia, ci sono alcune eccezioni, come descritto di seguito.


### Flusso di lavoro post-inizializzazione {#post-init}

Tutti i flussi di lavoro di adesione supportati da AccessEnabler presuppongono che in precedenza sia stato chiamato [`setRequestor()`](#setRequestor) per stabilire la tua identità. Esegui questa chiamata per fornire il tuo ID richiedente una sola volta, di solito durante la fase di inizializzazione/installazione dell&#39;applicazione.

Con i client nativi (ad esempio, AmazonFireOS), dopo la chiamata iniziale a [`setRequestor()`](#setRequestor), puoi scegliere come procedere:

- Puoi iniziare a effettuare chiamate di adesione immediatamente e consentire loro di essere messi in coda in modo silenzioso, se necessario.
- Oppure, puoi ricevere una conferma del successo/fallimento di [`setRequestor()`](#setRequestor) implementando il callback setRequestorComplete() .
- Oppure, fate entrambi.

Spetta a te decidere se attendere la notifica del successo di [`setRequestor()`](#setRequestor) o per utilizzare il meccanismo di coda chiamate di AccessEnabler. Poiché tutte le richieste di autorizzazione e autenticazione successive necessitano del requestor ID e delle relative informazioni di configurazione, la [`setRequestor()`](#setRequestor) blocca efficacemente tutte le chiamate API di autenticazione e autorizzazione fino al completamento dell&#39;inizializzazione.

### Flusso di lavoro di autenticazione iniziale generica {#generic}

Lo scopo di questo flusso di lavoro è quello di accedere a un utente con il suo MVPD.  Dopo l’accesso, il server di backend rilascia all’utente un token di autenticazione. Anche se l’autenticazione viene generalmente eseguita come parte del processo di autorizzazione, quanto segue descrive come l’autenticazione può funzionare in modo isolato e non include passaggi di autorizzazione.

Tieni presente che, mentre il seguente flusso di lavoro client nativo è diverso dal flusso di lavoro di autenticazione tipico basato su browser, i passaggi 1-5 sono gli stessi sia per i client nativi che per i client basati su browser:

1. La pagina o il lettore avvia il flusso di lavoro di autenticazione con una chiamata a [getAuthentication()](#getAuthN), che verifica la presenza di un token di autenticazione cache valido. Questo metodo ha un `redirectURL` parametro; se non fornisci un valore per `redirectURL`, dopo un’autenticazione riuscita, l’utente viene restituito all’URL da cui è stata inizializzata l’autenticazione.
1. AccessEnabler determina lo stato di autenticazione corrente. Se l&#39;utente è attualmente autenticato, AccessEnabler chiama il `setAuthenticationStatus()` funzione di callback, passaggio di uno stato di autenticazione che indica il successo (passaggio 7 qui sotto).
1. Se l&#39;utente non è autenticato, AccessEnabler continua il flusso di autenticazione determinando se l&#39;ultimo tentativo di autenticazione dell&#39;utente ha avuto successo con un MVPD specifico. Se un ID MVPD è memorizzato nella cache E `canAuthenticate` Il flag è true OPPURE è stato selezionato un MVPD utilizzando [`setSelectedProvider()`](#setSelectedProvider), all’utente non viene visualizzata una finestra di dialogo di selezione MVPD. Il flusso di autenticazione continua a utilizzare il valore memorizzato nella cache dell&#39;MVPD (cioè lo stesso MVPD utilizzato durante l&#39;ultima autenticazione riuscita). Viene effettuata una chiamata di rete al server back-end e l&#39;utente viene reindirizzato alla pagina di accesso MVPD (passaggio 6 qui sotto).
1. Se non è presente alcun ID MVPD nella cache e non è stato selezionato alcun MVPD utilizzando [`setSelectedProvider()`](#setSelectedProvider) O `canAuthenticate` il flag è impostato su false, il [`displayProviderDialog()`](#displayProviderDialog) chiamata di callback. Questo callback indirizza la pagina o il lettore a creare l&#39;interfaccia utente che presenta all&#39;utente un elenco di MVPD tra cui scegliere. Viene fornito un array di oggetti MVPD, contenente le informazioni necessarie per creare il selettore MVPD. Ogni oggetto MVPD descrive un&#39;entità MVPD e contiene informazioni come l&#39;ID dell&#39;MVPD (ad esempio, XFINITY, AT\&amp;T, ecc.) e l&#39;URL in cui è possibile trovare il logo MVPD.
1. Una volta selezionato un MVPD specifico, la pagina o il lettore devono informare AccessEnabler della scelta dell&#39;utente. Per i client non di Flash, una volta che l&#39;utente seleziona l&#39;MVPD desiderato, si informa AccessEnabler della selezione dell&#39;utente tramite una chiamata al [`setSelectedProvider()`](#setSelectedProvider) metodo . I client di Flash inviano invece una condivisione `MVPDEvent` di tipo &quot;`mvpdSelection`&quot;, passando il provider selezionato.
1. Per le applicazioni Amazon, la [`navigateToUrl()`](#navigagteToUrl) il callback verrà ignorato. La libreria di Access Enabler facilita l&#39;accesso a un controllo WebView comune per l&#39;autenticazione degli utenti.
1. Tramite il `WebView`, l’utente arriva sulla pagina di accesso dell’MVPD e immette le proprie credenziali. Durante questo trasferimento si verificano diverse operazioni di reindirizzamento. 
1. Una volta completata l&#39;autenticazione, WebView chiuderà e informerà AccessEnabler che l&#39;utente ha eseguito correttamente l&#39;accesso, AccessEnabler recupera il token di autenticazione effettivo dal server back-end. AccessEnabler chiama [`setAuthenticationStatus()`](#setAuthNStatus) callback con codice di stato 1 che indica il successo. Se si verifica un errore durante l&#39;esecuzione di questi passaggi, il [`setAuthenticationStatus()`](#setAuthNStatus) il callback viene attivato con un codice di stato pari a 0, insieme a un codice di errore corrispondente, che indica che l’utente non è autenticato.

### Flusso di lavoro di disconnessione {#logout}

Per i client nativi, gli accessi vengono gestiti in modo simile al processo di autenticazione descritto in precedenza. Seguendo questo pattern, AccessEnabler creerà un `WebView` controlla e caricherà il controllo con l’URL dell’endpoint di logout sul server back-end. Una volta completato il processo di logout, i token vengono cancellati.

Il flusso di logout è diverso dal flusso di autenticazione in quanto l’utente non è tenuto a interagire con il `WebView` in qualsiasi modo. Una volta completato l&#39;accesso, AccessEnabler chiama il `setAuthenticationStatus()` callback con codice di stato 0 che indica che l’utente non è autenticato.

## Token {#tokens}

### Definizioni e utilizzo {#definitions}

La soluzione di adesione all’autenticazione di Primetime ruota attorno alla generazione di pezzi di dati specifici (token) generati dall’autenticazione di Primetime al completamento dei flussi di lavoro di autenticazione e autorizzazione. Questi token vengono memorizzati localmente sul dispositivo Amazon FireOS del client.

I gettoni hanno una durata di vita limitata; alla scadenza, i token devono essere riemessi mediante il riavvio dei flussi di lavoro di autenticazione e/o autorizzazione.

Durante i flussi di lavoro di adesione sono disponibili tre tipi di token:

- **Token di autenticazione** - Il risultato finale del flusso di lavoro di autenticazione dell&#39;utente sarà un GUID di autenticazione che AccessEnabler può utilizzare per eseguire query di autorizzazione per conto dell&#39;utente. Questo GUID di autenticazione avrà un valore TTL (time-to-live) associato che potrebbe essere diverso dalla sessione di autenticazione dell&#39;utente stessa. Primetime Authentication genera un token di autenticazione mediante il binding del GUID di autenticazione al dispositivo che avvia le richieste di autenticazione.
- **Token di autorizzazione** - Consente l&#39;accesso a una specifica risorsa protetta identificata da un `resourceID`. Si tratta di una concessione di autorizzazione rilasciata dalla parte che ha rilasciato l&#39;autorizzazione insieme all&#39;originale `resourceID`. Queste informazioni sono associate al dispositivo che avvia la richiesta.
- **Token multimediale di breve durata** - AccessEnabler concede l&#39;accesso all&#39;applicazione di hosting per una determinata risorsa restituendo un Media Token di breve durata. Questo token viene generato in base al token di autorizzazione precedentemente acquisito per quella specifica risorsa. Inoltre, questo token non è associato al dispositivo e l’intervallo di vita associato è significativamente più breve (impostazione predefinita: 5 minuti).

Dopo l’autenticazione e l’autorizzazione riuscite, l’autenticazione di Primetime rilascerà l’autenticazione, l’autorizzazione e i token multimediali di breve durata. Questi token devono essere memorizzati nella cache del dispositivo dell’utente e utilizzati per la durata della loro durata di vita associata.

### Linee guida sulla memorizzazione in cache {#caching}


#### Token di autenticazione

- **AccessEnabler 1.10.1 per FireOS **si basa su AccessEnabler per Android 1.9.1 - Questo SDK introduce un nuovo metodo di archiviazione dei token, che abilita più bucket Programmer-MVPD e quindi più token di autenticazione. 

#### Token di autorizzazione

In qualsiasi momento, AccessEnabler memorizza nella cache solo un token di autorizzazione per risorsa. Possono essere presenti più token di autorizzazione nella cache, ma sono associati a risorse diverse. Ogni volta che viene rilasciato un nuovo token di autorizzazione e ne esiste già uno vecchio per la stessa risorsa, il nuovo token sovrascrive il valore cache esistente.

#### Token multimediale 

Il token multimediale di breve durata NON deve essere memorizzato nella cache. Il token multimediale deve essere recuperato dal server ogni volta che viene chiamata un’API di autorizzazione, perché è limitato all’utilizzo una tantum.

### Persistenza {#persistence}

I token devono essere costanti in esecuzioni consecutive della stessa applicazione. Ciò significa che, una volta acquisiti i token di autenticazione e autorizzazione e quando l’utente chiude l’applicazione, gli stessi token sono disponibili per l’applicazione quando l’utente riapre l’applicazione. Inoltre, è auspicabile che questi token siano persistenti in più applicazioni. In altre parole, dopo che un utente utilizza un&#39;applicazione per accedere con un provider di identità specifico (ottenendo con successo i token di autenticazione e autorizzazione), gli stessi token possono essere utilizzati tramite un&#39;applicazione diversa e all&#39;utente non viene più richiesto di specificare le credenziali quando effettua l&#39;accesso tramite lo stesso provider di identità.

Questo tipo di flusso di lavoro di autenticazione/autorizzazione è ciò che rende la soluzione di autenticazione Primetime una vera implementazione TV-Everywhere. Dal punto di vista puramente ingegneristico, la libreria di Android AccessEnabler si occupa dei problemi di condivisione dei dati tra applicazioni memorizzando i dati del token in un file di database che si trova sullo storage esterno. Questa risorsa condivisa a livello di sistema fornisce gli ingredienti chiave che consentono l’implementazione del caso d’uso dei token persistenti desiderati:

- Supporto per lo storage strutturato - Lo storage dei token di autenticazione Primetime non è solo una semplice struttura di memoria lineare simile al buffer. Fornisce un meccanismo di archiviazione simile a un dizionario che consente l&#39;indicizzazione dei dati in base ai valori chiave specificati dall&#39;utente.
- Supporto della persistenza dei dati utilizzando il file system sottostante - Il contenuto del file di database viene mantenuto per impostazione predefinita e i dati vengono salvati nella memoria esterna del dispositivo.

Una volta inserito un token nella cache del token, la sua validità verrà controllata in momenti diversi dalla libreria AccessEnabler.  Un token valido è definito come:

- TTL del token non scaduto
- L&#39;emittente del token è incluso nell&#39;elenco dei provider di identità consentiti

L&#39;archiviazione dei token può supportare più combinazioni Programmer-MVPD, basandosi su una struttura di mappa nidificata a più livelli che può contenere più token di autenticazione. Questo nuovo archivio non influisce in alcun modo sull&#39;API pubblica di AccessEnabler e non richiede modifiche sul lato del programmatore. Ecco un esempio che illustra questa nuova funzionalità:

1. Apri App1 (sviluppato da Programmer1).
1. Autentica con MVPD1 (integrato con Programmer1).
1. Sospendi / chiudi l&#39;applicazione corrente e apri App2 (sviluppato da Programmer2).
1. Supponiamo che Programmer2 non sia integrato con MVPD2; pertanto, l&#39;utente NON sarà autenticato in App2.
1. Autentica con MVPD2 (integrato con Programmer2) in App2.
1. Torna ad App1; l’utente sarà ancora autenticato con Programmer1.

### Formato {#format}

#### Token di autenticazione {#authn_token}

L’elenco seguente presenta il formato del token di autenticazione:

```JSON
    <signatureInfo>base64(...)<signatureInfo>
    <simpleAuthenticationToken>
        <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
        <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
        <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
        <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
        <simpleTokenMsoID>Adobe</simpleTokenMsoID>
        <simpleTokenDeviceID>
            <simpleTokenFingerprint>
                HASH(true device identification info)
            </simpleTokenFingerprint>
        </simpleTokenDeviceID>   
    </simpleAuthenticationToken>
```
 

#### Token di autorizzazione {#authz_token}

L’elenco seguente presenta il formato del token di autorizzazione:

```JSON
    <signatureInfo>base64(...)<signatureInfo>
    <simpleAuthorizationToken>
        <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
        <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
        <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
        <simpleTokenMsoID>Adobe</simpleTokenMsoID>
        <simpleTokenDeviceID>
            <simpleTokenFingerprint>
                HASH(true device identification info)
            </simpleTokenFingerprint>
        </simpleTokenDeviceID>
    </simpleAuthorizationToken>
```


#### Token multimediale breve {#short_media_token}

L’elenco seguente presenta il formato del token per contenuti multimediali brevi.  Questo token è esposto all&#39;applicazione del programmatore.  Viene passato all&#39;applicazione del programmatore al termine di un processo di adesione riuscito:

```JSON
    <signatureInfo>signature<signatureInfo>
    <shortAuthorizationToken>
      <sessionGUID>session_guid</sessionGUID>
      <requestorID>requestor_id</requestorID>
      <resourceID>resource_id</resourceID>
      <ttl>ttl_in_ms</ttl>
      <issueTime>issue_time</issueTime>
      <mvpdId>mvpd_id</mvpdId>
      <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
    </shortAuthorizationToken>
```
 

#### Binding dei dispositivi {#device_binding}

Negli elenchi XML di cui sopra, prendi nota del tag denominato `simpleTokenFingerprint`. Lo scopo di questo tag è quello di contenere informazioni native sull’identificazione degli ID dispositivo. La libreria AccessEnabler è in grado di ottenere tali informazioni di personalizzazione e di renderle disponibili ai servizi di autenticazione Primetime durante le chiamate di adesione. Il servizio utilizzerà queste informazioni e le incorporerà nei token effettivi, così da collegare efficacemente i token a un dispositivo specifico. L’obiettivo finale è rendere i token non trasferibili tra dispositivi diversi.

Negli elenchi XML di cui sopra, prendi nota del tag simpleTokenFingerprint. Lo scopo di questo tag è quello di contenere informazioni native sull’identificazione degli ID dispositivo. La libreria AccessEnabler è in grado di ottenere tali informazioni di personalizzazione e di renderle disponibili ai servizi di autenticazione Primetime durante le chiamate di adesione. Il servizio utilizzerà queste informazioni e le incorporerà nei token effettivi, così da collegare efficacemente i token a un dispositivo specifico. L’obiettivo finale è rendere i token non trasferibili tra dispositivi diversi.

Poiché si tratta ovviamente di una funzione correlata alla sicurezza, queste informazioni sono intrinsecamente &quot;sensibili&quot; dal punto di vista della sicurezza. Di conseguenza, queste informazioni devono essere protette da manomissioni e intercettazioni. Il problema delle intercettazioni viene risolto inviando le richieste di autenticazione/autorizzazione tramite il protocollo HTTPS. La protezione da manomissione viene gestita tramite la firma digitale delle informazioni di identificazione del dispositivo. La libreria AccessEnabler calcola un ID dispositivo dalle informazioni fornite dal dispositivo, quindi invia l&#39;ID dispositivo &quot;nel limpido&quot; ai server di autenticazione Primetime come parametro di richiesta.  I server di autenticazione Primetime firmano digitalmente l&#39;ID dispositivo con la chiave privata di Adobe e lo aggiungono al token di autenticazione restituito ad AccessEnabler. Pertanto l’ID dispositivo è associato al token di autenticazione.  Durante il flusso di autorizzazione, AccessEnabler invia nuovamente l&#39;ID dispositivo in modo chiaro, insieme al token di autenticazione.  In caso di errore del processo di convalida si verifica automaticamente un errore dei flussi di lavoro di autenticazione/autorizzazione.  I server di autenticazione Primetime applicano la chiave privata all&#39;ID dispositivo e la confrontano con il valore nel token di autenticazione.  Se non corrispondono, il flusso di adesione non riesce.
