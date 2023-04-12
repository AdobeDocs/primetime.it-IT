---
title: Panoramica dell'SDK per iOS/tvOS
description: Panoramica dell'SDK per iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 0%

---


# Panoramica dell&#39;SDK per iOS/tvOS {#iostvos-sdk-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


</br>


## Introduzione {#intro}

iOS AccessEnabler è una libreria Objective-C iOS/tvOS che consente alle app mobili di utilizzare l&#39;autenticazione Adobe Primetime per i servizi di adesione di TV Everywhere. L&#39;attuazione consiste nella *AccessEnabler* l&#39;interfaccia che definisce l&#39;API di adesione e *EntitlementDelegate* e *[EntitlementStatus](#ios%20entitlement%20status)* protocolli che descrivono i callback attivati dalla libreria. L&#39;interfaccia e il protocollo sono indicati con un nome comune: libreria AccessEnabler.

## Requisiti di iOS e tvOS {#reqs}

Per i requisiti tecnici correnti relativi alla piattaforma iOS e tvOS e all&#39;autenticazione Primetime, vedi [Requisiti di piattaforma/dispositivo/strumento](#ios)e consulta le note sulla versione incluse nel download dell’SDK. Nel resto della pagina, vedrai le sezioni che annotano le modifiche che si applicano a specifiche versioni SDK e versioni successive. Ad esempio, una nota legittima riguardante l&#39;SDK 1.7.5:

## Informazioni sui flussi di lavoro dei client nativi {#flows}

I flussi di lavoro client nativi sono generalmente uguali o molto simili a quelli dei client di autenticazione Primetime basati su browser. Tuttavia, ci sono alcune eccezioni, come descritto di seguito.

- [Flusso di lavoro post-inizializzazione](#post-init)
- [Flusso di lavoro di autenticazione iniziale generica](#generic)
- [Flusso di lavoro di disconnessione](#logout)


### Flusso di lavoro post-inizializzazione {#post-init}

Tutti i flussi di lavoro di adesione supportati da AccessEnabler presuppongono che in precedenza sia stato chiamato [`setRequestor()`](#setReq) per stabilire la tua identità. Esegui questa chiamata per fornire il tuo ID richiedente una sola volta, di solito durante la fase di inizializzazione/installazione dell&#39;applicazione.


Con un client nativo iOS, dopo la chiamata iniziale a [`setRequestor()`](#setReq), puoi scegliere come procedere:

- Puoi iniziare a effettuare chiamate di adesione immediatamente e consentire loro di essere messi in coda in modo silenzioso, se necessario.

- Puoi ricevere una conferma del successo/fallimento di [`setRequestor()`](#setReq) attuando [`setRequestorComplete()`](#setReqComplete) callback.

- Potete fare entrambe le cose sopra.

Puoi scegliere di fare in modo che l’app attenda la notifica del successo di [`setRequestor()`](#setReq) o fare affidamento sul meccanismo di coda delle chiamate di AccessEnabler. Poiché tutte le richieste di autorizzazione e autenticazione successive necessitano del requestor ID e delle relative informazioni di configurazione, la [`setRequestor()`](#setReq) blocca efficacemente tutte le chiamate API di autenticazione e autorizzazione fino al completamento dell&#39;inizializzazione.

 

### Flusso di lavoro di autenticazione iniziale generica {#generic}

Lo scopo di questo flusso di lavoro è quello di accedere a un utente con il suo MVPD. Dopo l’accesso, il server di backend rilascia all’utente un token di autenticazione. Anche se l’autenticazione viene generalmente eseguita come parte del processo di autorizzazione, quanto segue descrive come l’autenticazione può funzionare in modo isolato e non include passaggi di autorizzazione.

Sebbene questo flusso di lavoro sia diverso per i client nativi dal flusso di lavoro di autenticazione tipico basato su browser, i passaggi 1-5 sono gli stessi per i client nativi e per i client basati su browser.

1. L&#39;applicazione avvia il flusso di lavoro di autenticazione con una chiamata a AccessEnabler `getAuthentication() `Metodo API, che verifica la presenza di un token di autenticazione valido nella cache.
1. Se l&#39;utente è attualmente autenticato, AccessEnabler chiama il [`setAuthenticationStatus()`](#setAuthNStatus) funzione di callback, passaggio di uno stato di autenticazione che indica il successo e fine del flusso.
1. Se l&#39;utente non è attualmente autenticato, AccessEnabler continua il flusso di autenticazione determinando se l&#39;ultimo tentativo di autenticazione dell&#39;utente è riuscito con un MVPD specifico. Se un ID MVPD è memorizzato nella cache E `canAuthenticate` Il flag è true OPPURE è stato selezionato un MVPD utilizzando [`setSelectedProvider()`](#setSelProv), all’utente non viene visualizzata una finestra di dialogo di selezione MVPD. Il flusso di autenticazione continua a utilizzare il valore memorizzato nella cache dell&#39;MVPD (cioè lo stesso MVPD utilizzato durante l&#39;ultima autenticazione riuscita). Viene effettuata una chiamata di rete al server back-end e l&#39;utente viene reindirizzato alla pagina di accesso MVPD (passaggio 6 qui sotto).
1. Se non è presente alcun ID MVPD nella cache e non è stato selezionato alcun MVPD utilizzando [`setSelectedProvider()`](#setSelProv) O `canAuthenticate` il flag è impostato su false, il [`displayProviderDialog()`](#dispProvDialog) chiamata di callback. Questo callback indica all’applicazione di creare l’interfaccia utente che presenta all’utente un elenco di MVPD tra cui scegliere. Viene fornito un array di oggetti MVPD, contenente le informazioni necessarie per creare il selettore MVPD. Ogni oggetto MVPD descrive un&#39;entità MVPD e contiene informazioni come l&#39;ID dell&#39;MVPD (ad esempio, XFINITY, AT\&amp;T, ecc.) e l&#39;URL in cui è possibile trovare il logo MVPD.
1. Una volta selezionato un MVPD specifico, l&#39;applicazione deve informare AccessEnabler della scelta dell&#39;utente. Una volta selezionato l&#39;MVPD desiderato, si informa AccessEnabler della selezione dell&#39;utente tramite una chiamata al [`setSelectedProvider()`](#setSelProv) metodo .
1. iOS AccessEnabler chiama il tuo `navigateToUrl:` callback o `navigateToUrl:useSVC:` callback per reindirizzare l&#39;utente alla pagina di accesso MVPD. Attivando una di queste opzioni, AccessEnabler invia una richiesta all&#39;applicazione per creare una `UIWebView/WKWebView or SFSafariViewController` e per caricare l&#39;URL fornito nel callback `url` parametro . Si tratta dell’URL dell’endpoint di autenticazione sul server back-end. Per tvOS AccessEnabler, il [status()](#status_callback_implementation) chiamata di callback con un `statusDictionary` e il polling per l&#39;autenticazione a seconda schermata viene avviato immediatamente. La `statusDictionary` contiene `registration code` deve essere utilizzato per l’autenticazione a seconda schermata. 
1. Nel caso di iOS AccessEnabler, l&#39;utente arriva sulla pagina di accesso dell&#39;MVPD per inserire le sue credenziali attraverso il supporto dell&#39;applicazione `UIWebView/WKWebView or SFSafariViewController `controller. Durante questo trasferimento si verificano diverse operazioni di reindirizzamento e l&#39;applicazione deve monitorare gli URL caricati dal controller durante le operazioni di reindirizzamento multiple.
1. Nel caso di iOS AccessEnabler, quando il `UIWebView/WKWebView or SFSafariViewController` il controller carica un URL personalizzato specifico che l&#39;applicazione deve chiudere il controller e chiamare AccessEnabler&#39;s `handleExternalURL:url `Metodo API. Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che il flusso di autenticazione è stato completato e che è sicuro chiudere il `UIWebView/WKWebView or SFSafariViewController` controller. Nel caso in cui l&#39;applicazione debba utilizzare un `SFSafariViewController `l&#39;URL personalizzato specifico viene definito dalla `application's custom scheme` (ad esempio: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), altrimenti questo URL personalizzato specifico viene definito dalla `ADOBEPASS_REDIRECT_URL` costante (ovvero `adobepass://ios.app`).
1. Una volta chiusa l&#39;applicazione, `UIWebView/WKWebView or SFSafariViewController` controller e chiama AccessEnabler&#39;s `handleExternalURL:url `Metodo API, AccessEnabler recupera il token di autenticazione dal server back-end e informa l&#39;applicazione che il flusso di autenticazione è completo. AccessEnabler chiama [`setAuthenticationStatus()`](#setAuthNStatus) callback con codice di stato 1 che indica il successo. Se si verifica un errore durante l&#39;esecuzione di questi passaggi, il [`setAuthenticationStatus()`](#setAuthNStatus) il callback viene attivato con un codice di stato pari a 0 che indica un errore di autenticazione e un codice di errore corrispondente.


>[!WARNING]
>
> Durante i passaggi in cui AccessEnabler rinuncia al controllo sull&#39;app (ovvero, quando viene visualizzata la finestra di dialogo di selezione del provider, o quando viene visualizzato UIWebView/WKWebView o SFSafariViewController) l&#39;utente ha l&#39;opportunità di annullare il flusso di autenticazione. In queste situazioni, l&#39;app è responsabile dell&#39;informazione di AccessEnabler su questo evento e della chiamata al [`setSelectedProvider()`](#setSelProv) Metodo API, passando null come parametro. In questo modo AccessEnabler può ripulire il proprio stato interno e ripristinare il flusso di autenticazione. Su tvOS, è possibile utilizzare lo stesso metodo per annullare il polling di autenticazione.


### Flusso di lavoro di disconnessione {#logout}

Per i client nativi, la disconnessione viene gestita in modo simile al processo di autenticazione descritto in precedenza.

1. L&#39;applicazione avvia il flusso di lavoro di logout con una chiamata a AccessEnabler `logout() `Metodo API. La disconnessione è il risultato di una serie di operazioni di reindirizzamento HTTP a causa del fatto che l&#39;utente deve essere disconnesso sia dai server di autenticazione Primetime che dai server MVPD. Poiché questo flusso non può essere completato con una semplice richiesta HTTP inviata dalla libreria AccessEnabler, un `UIWebView/WKWebView or SFSafariViewController` è necessario creare un&#39;istanza del controller per poter seguire le operazioni di reindirizzamento HTTP.

1. Viene utilizzato un pattern simile al flusso di autenticazione. iOS AccessEnabler attiva il `navigateToUrl:` callback o `navigateToUrl:useSVC:` per creare un `UIWebView/WKWebView or SFSafariViewController` e per caricare l&#39;URL fornito nel callback `url` parametro . Si tratta dell’URL dell’endpoint di logout sul server back-end. Per tvOS AccessEnabler né il `navigateToUrl:` callback o `navigateToUrl:useSVC:` chiamata di callback.

1. Mentre passa attraverso diversi reindirizzamenti, l&#39;applicazione deve monitorare l&#39;attività del `UIWebView/WKWebView or SFSafariViewController `controlla e rileva il momento in cui carica un URL personalizzato specifico. Tieni presente che questo URL personalizzato specifico non è in realtà valido e non è destinato al controller per caricarlo effettivamente. Deve essere interpretato solo dall&#39;applicazione come un segnale che il flusso di logout è stato completato e che è sicuro chiudere il controller. Quando il controller carica questo URL personalizzato specifico, l&#39;applicazione deve chiudere il controller e chiamare AccessEnabler&#39;s `handleExternalURL:url `Metodo API. Nel caso in cui l&#39;applicazione debba utilizzare un `SFSafariViewController `l&#39;URL personalizzato specifico viene definito dalla `application's custom scheme` (ad esempio`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), altrimenti questo URL personalizzato specifico viene definito dalla ` ADOBEPASS_REDIRECT_URL  `costante (ovvero `adobepass://ios.app`).

1. Alla fine, AccessEnabler chiamerà il [`setAuthenticationStatus()`](#setAuthNStatus) callback con un codice di stato pari a 0, che indica il successo del flusso di logout.

Il flusso di logout è diverso dal flusso di autenticazione in quanto l’utente non è tenuto a interagire con il `UIWebView/WKWebView or SFSafariViewController`  in qualsiasi modo. Pertanto, Adobe consiglia di rendere il controllo invisibile (cioè nascosto) durante il processo di logout.

## Token {#tokens}

- [Definizioni e utilizzo](#definitions)
- [Linee guida sulla memorizzazione in cache](#caching)
- [Persistenza](#persistence)
- [Formato](#format)
- [Binding dei dispositivi](#device_binding)


### Definizioni e utilizzo {#definitions}

La soluzione di adesione all’autenticazione di Primetime ruota attorno alla generazione di pezzi di dati specifici (token) generati dall’autenticazione di Primetime al completamento dei flussi di lavoro di autenticazione e autorizzazione. Questi token vengono memorizzati localmente sul dispositivo iOS del client.

 

I gettoni hanno una durata di vita limitata; alla scadenza, i token devono essere riemessi mediante il riavvio dei flussi di lavoro di autenticazione e/o autorizzazione.

 

Durante i flussi di lavoro di adesione sono disponibili tre tipi di token:

- **Token di autenticazione:** Il risultato finale del flusso di lavoro di autenticazione dell&#39;utente sarà un GUID di autenticazione che AccessEnabler può utilizzare per eseguire query di autorizzazione per conto dell&#39;utente. Questo GUID di autenticazione avrà un valore TTL (time-to-live) associato che potrebbe essere diverso dalla sessione di autenticazione dell&#39;utente stessa. Verrà generato un token di autenticazione mediante il binding del GUID di autenticazione al dispositivo che avvia le richieste di autenticazione.
- **Token di autorizzazione:** Consente di accedere a una risorsa protetta specifica identificata da un resourceID univoco. È costituito da una concessione di autorizzazione rilasciata dalla parte che ha rilasciato l’autorizzazione insieme all’ID risorsa originale. Queste informazioni sono associate al dispositivo che avvia la richiesta.
- **Token multimediale breve:** AccessEnabler concede l&#39;accesso all&#39;applicazione di hosting per una determinata risorsa restituendo un token multimediale di breve durata. Questo token viene generato in base al token di autorizzazione precedentemente acquisito per quella specifica risorsa. Inoltre, questo token non è associato al dispositivo e l’intervallo di vita associato è significativamente più breve (impostazione predefinita: 5 minuti).

Dopo l’autenticazione e l’autorizzazione riuscite, l’autenticazione di Primetime rilascerà l’autenticazione, l’autorizzazione e i token multimediali di breve durata. Questi token devono essere memorizzati nella cache del dispositivo dell’utente e utilizzati per la durata della loro durata di vita associata.

 

### Linee guida sulla memorizzazione in cache {#caching}

- Token di autenticazione
- Token di autorizzazione
- Token multimediale di breve durata


#### Token di autenticazione

- **AccessEnabler 1.7:** Questo SDK introduce un nuovo metodo di archiviazione dei token, che abilita più bucket Programmer-MVPD e quindi più token di autenticazione. Ora, lo stesso layout di archiviazione viene utilizzato sia per lo scenario &quot;Authentication per Requestor&quot; sia per il normale flusso di autenticazione. L’unica differenza tra i due è rappresentata dal modo in cui viene eseguita l’autenticazione: &quot;Authentication per Requestor&quot; contiene un nuovo miglioramento (Passive Authentication) che consente ad AccessEnabler di eseguire l&#39;autenticazione back-channel in base all&#39;esistenza di un token di autenticazione nell&#39;archivio (per un programmatore diverso). L’utente deve eseguire l’autenticazione solo una volta e questa sessione verrà utilizzata per ottenere token di autenticazione in altre app. Questo flusso del back-channel avviene durante il [`setRequestor()`](#setReq) chiamare ed è principalmente trasparente per il programmatore. **Vi è tuttavia un requisito importante: il programmatore DEVE chiamare setRequestor() dal thread dell&#39;interfaccia utente principale.**
- **AccessEnabler 1.6 e versioni precedenti:** Il modo in cui i token di autenticazione sono memorizzati nella cache del dispositivo dipende da &quot;**Autenticazione per richiedente&quot;** flag associato all&#39;MVPD corrente:

<!-- end list -->

1. Se la funzione &quot;Autenticazione per richiedente&quot; è disabilitata, un singolo token di autenticazione verrà memorizzato localmente nel pannello di controllo globale; questo token verrà condiviso tra tutte le applicazioni integrate con l&#39;MVPD corrente.
1. Se la funzione &quot;Autenticazione per richiedente&quot; è abilitata, un token verrà associato in modo esplicito al programmatore che ha eseguito il flusso di autenticazione (il token non verrà memorizzato nel pannello di controllo globale, ma in un file privato visibile solo all&#39;applicazione del programmatore). In particolare, l&#39;accesso Single Sign-On (SSO) tra diverse applicazioni sarà disattivato; l’utente dovrà eseguire esplicitamente il flusso di autenticazione quando passa a una nuova app (purché il programmatore della seconda app sia integrato con l’MVPD corrente e non esista alcun token di autenticazione per quel programmatore nella cache locale).

 

#### Token di autorizzazione

In qualsiasi momento, AccessEnabler memorizza nella cache solo un token di autorizzazione PER RISORSA. Possono essere presenti più token di autorizzazione nella cache, ma sono associati a risorse diverse. Ogni volta che viene rilasciato un nuovo token di autorizzazione e ne esiste già uno vecchio per *la stessa risorsa*, il nuovo token sovrascrive il valore cache esistente.

 

#### Token multimediale

Il token multimediale di breve durata NON deve essere memorizzato nella cache. Il token multimediale deve essere recuperato dal server ogni volta che viene chiamata un’API di autorizzazione, perché è limitato all’utilizzo una tantum.

 

### Persistenza {#persistence}

I token devono essere costanti in esecuzioni consecutive della stessa applicazione. Ciò significa che, una volta acquisiti i token di autenticazione e autorizzazione e quando l’utente chiude l’applicazione, gli stessi token sono disponibili per l’applicazione quando l’utente riapre l’applicazione. Inoltre, è auspicabile che questi token siano persistenti in più applicazioni. In altre parole, dopo che un utente utilizza un&#39;applicazione per accedere con un provider di identità specifico (ottenendo con successo i token di autenticazione e autorizzazione), gli stessi token possono essere utilizzati tramite un&#39;applicazione diversa e all&#39;utente non viene più richiesto di specificare le credenziali quando effettua l&#39;accesso tramite lo stesso provider di identità. Questo tipo di flusso di lavoro di autenticazione/autorizzazione è ciò che rende la soluzione di autenticazione Primetime una vera implementazione TV-Everywhere. 

 

## iOS

La libreria iOS AccessEnabler aggira i problemi della condivisione di dati tra applicazioni memorizzando i dati del token in una struttura di dati &quot;simile agli Appunti&quot; denominata *cartone*. Questa risorsa condivisa a livello di sistema fornisce gli ingredienti chiave che consentono l’implementazione del caso di utilizzo dei token persistenti desiderato:

- **Supporto per lo storage strutturato** - La scheda pasta non è solo una semplice struttura di memoria lineare simile al buffer. Fornisce un meccanismo di archiviazione simile a un dizionario che consente l&#39;indicizzazione dei dati in base ai valori chiave specificati dall&#39;utente.
- **Supporto della persistenza dei dati utilizzando il file system sottostante** - Il contenuto della struttura della scheda di incolla può essere contrassegnato come persistente, nel qual caso i dati vengono salvati nella memoria interna del dispositivo.

 

Una volta inserito un token nella cache del token, la sua validità verrà controllata in momenti diversi dalla libreria AccessEnabler.  Un token valido è definito come:

- TTL del token non scaduto.
- L’emittente del token è incluso nell’elenco dei provider di identità consentiti.

 

## tvOS

Poiché in tvOS il tavolo di montaggio non è disponibile, la libreria AccessEnabler tvOS utilizza NsUserDefaults come opzione di archiviazione. Questo risolve il problema della persistenza dei token di autenticazione e autorizzazione, ma le informazioni archiviate non possono essere condivise tra diverse applicazioni.

 

**Modifiche al tavolo di pasto iOS 10 -** Durante l’aggiornamento da una versione precedente di iOS, il pannello di controllo verrà cancellato. Ciò significa che tutte le applicazioni devono essere nuovamente autenticate.

 

**Modifiche al tavolo di montaggio di iOS 7 -** A causa dei cambiamenti nella modalità di funzionamento dei pannelli di controllo su iOS 7, ci sarà un accesso SSO incrociato limitato tra le applicazioni in esecuzione su iOS 7. Applicazioni uguali `<Bundle Seed ID>`(noto anche come `<Team ID>`) condividerà i token, il che significa che le app A1 e A2 dello stesso programmatore X condivideranno i token, mentre l&#39;app A1 (programmatore X) e l&#39;app A3 (programmatore Y) non condivideranno i token. 

- Bundle Seed ID/Team ID è lo stesso tra 2 app se sono generate dallo stesso profilo di provisioning. Per ulteriori informazioni, consulta questo link:
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- Questa limitazione &quot;Cross SSO&quot; sarà presente in iOS 7 indipendentemente dall’SDK di autenticazione Primetime utilizzato. 

Leggi questa nota tecnica per ulteriori informazioni sulla configurazione di SSO su iOS 7 e superiore (la nota tecnica si applica per Access Enabler v1.8 e superiore): <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### Archiviazione token (AccessEnabler 1.7)

A partire da AccessEnabler 1.7, lo storage dei token può supportare più combinazioni Programmer-MVPD, basandosi su una struttura di mappa nidificata a più livelli che può contenere più token di autenticazione. Questo nuovo archivio non influisce in alcun modo sull&#39;API pubblica di AccessEnabler e non richiede modifiche sul lato del programmatore. Ecco un esempio che illustra questa nuova funzionalità:

1. Apri App1 (sviluppato da Programmer1).
1. Autentica con MVPD1 (integrato con Programmer1).
1. Sospendi / chiudi l&#39;applicazione corrente e apri App2 (sviluppato da Programmer2).
1. Supponiamo che Programmer2 non sia integrato con MVPD2; pertanto, l&#39;utente NON sarà autenticato in App2.
1. Autentica con MVPD2 (integrato con Programmer2) in App2.
1. Torna ad App1; l’utente sarà ancora autenticato con Programmer1.

Nelle versioni precedenti di AccessEnabler, il passaggio 6 eseguiva il rendering dell&#39;utente come non autenticato, perché l&#39;archiviazione dei token in precedenza supportava un solo token di autenticazione.

 

La disconnessione da una sessione Programmer / MVPD cancellerà l&#39;intero spazio di archiviazione sottostante, inclusi tutti gli altri token di autenticazione Programmer / MVPD sul dispositivo. D&#39;altra parte, annullare il flusso di autenticazione (richiamando [`setSelectedProvider(null)`](#setSelProv)) NON cancella lo storage sottostante, ma influenzerà solo l&#39;attuale tentativo di autenticazione del programmatore / MVPD (cancellando il MVPD per il programmatore corrente).

 

### Importazione token (AccessEnabler 1.7)

Un’altra funzionalità relativa allo storage inclusa in AccessEnabler 1.7 consente di importare token di autenticazione dalle aree di storage più vecchie. Questo &quot;Token Importer&quot; aiuta a raggiungere la compatibilità tra le versioni consecutive di AccessEnabler, mantenendo lo stato SSO anche quando la versione di archiviazione viene aggiornata. L’importazione viene eseguita durante il [`setRequestor()`](#setReq) Flusso ed esecuzione nei due scenari seguenti (partendo dal presupposto che nello storage corrente non sia presente alcun token di autenticazione valido per il programmatore corrente):

- La prima installazione di un&#39;app 1.7 sviluppata da un programmatore specifico
- Percorso di aggiornamento di un AccessEnabler futuro che utilizza un nuovo archivio

L&#39;operazione di importazione è trasparente per il programmatore e non richiede alcuna modifica del codice nell&#39;applicazione client.

 

### Sanitizer token (AccessEnabler 1.7.5)

Da AccessEnabler 1.7.5 in avanti, questo servizio viene eseguito su [`setRequestor()`](#setReq)`. `È stato sviluppato grazie allo switch iOS 7 dall&#39;indirizzo MAC WiFi all&#39;identificatore IDFA per il tracciamento. Lo strumento di pulizia assicura che l&#39;archiviazione corrente contenga solo token di autenticazione validi (validi in termini di ID dispositivo, precedentemente calcolato utilizzando l&#39;indirizzo MAC, prima di iOS7). Il Token Sanitizer rimuove tutti i token non validi. 

 

Il servizio Token Sanitizer è più utile quando un&#39;applicazione AccessEnabler 1.7.5 viene utilizzata su iOS 6 e l&#39;utente si aggiorna ad iOS 7. In questo caso, tutti i token di autenticazione ottenuti su iOS 6 non saranno validi (a causa della modifica dell&#39;algoritmo ID dispositivo dall&#39;utilizzo dell&#39;indirizzo MAC all&#39;identificatore IDFA). L&#39;utilità di pulizia cancella tutti i token non validi e l&#39;utente non sarà quindi autenticato. 

 

Senza il Token Sanitizer che rimuove i token non validi, AccessEnabler non otterrà le autorizzazioni a causa della presenza di token di autenticazione non validi. Questo risulterebbe difficile per l&#39;utente finale eseguire il debug, in quanto i messaggi di errore di autorizzazione possono essere crittografati e non troppo utili per determinare quale causa il problema. 

 

### Formato {#format}

- [Token AuthN](#authn_token)
- [Token AuthZ](#authz_token)
- [Token multimediale breve](#short_token)
- [Binding dei dispositivi](#device_binding)


Il formato dei token AuthN e AuthZ è incluso qui solo per informazioni di sfondo. La struttura di questi token può essere modificata in qualsiasi momento dall’autenticazione Primetime. I programmatori non devono conoscere la struttura esatta dei token AuthN e AuthZ per implementare le proprie app, in quanto i token AuthN e AuthZ non sono esposti sul dispositivo locale. Token per contenuti multimediali brevi *è* esposto all&#39;applicazione del programmatore.

 

#### Token di autenticazione {#authn_token}

L’elenco seguente presenta il formato del token di autenticazione:

```
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

```
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
 

#### Token multimediale breve {#short_token}

L’elenco seguente presenta il formato del token per contenuti multimediali brevi. Questo token è esposto all&#39;applicazione del programmatore. Viene passato all&#39;applicazione del programmatore al termine di un processo di adesione riuscito:

```
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
 

### Binding dei dispositivi {#device_binding}

Negli elenchi XML di cui sopra, prendi nota del tag denominato `simpleTokenFingerprint`. Lo scopo di questo tag è quello di contenere informazioni native sull’identificazione degli ID dispositivo. La libreria AccessEnabler è in grado di ottenere tali informazioni di personalizzazione e di renderle disponibili ai servizi di autenticazione Primetime durante le chiamate di adesione. Il servizio utilizzerà queste informazioni e le incorporerà nei token effettivi, così da collegare efficacemente i token a un dispositivo specifico. L’obiettivo finale è rendere i token non trasferibili tra dispositivi diversi.

 

Poiché si tratta ovviamente di una funzione correlata alla sicurezza, queste informazioni sono intrinsecamente &quot;sensibili&quot; dal punto di vista della sicurezza. Di conseguenza, queste informazioni devono essere protette da manomissioni e intercettazioni. Il problema delle intercettazioni viene risolto inviando le richieste di autenticazione/autorizzazione tramite il protocollo HTTPS. La protezione da manomissione viene gestita tramite la firma digitale delle informazioni di identificazione del dispositivo. La libreria AccessEnabler calcola un ID dispositivo dalle informazioni fornite dal dispositivo, quindi invia l&#39;ID dispositivo &quot;nel limpido&quot; ai server di autenticazione Primetime come parametro di richiesta. I server di autenticazione Primetime firmano digitalmente l&#39;ID dispositivo con la chiave privata di Adobe e lo aggiungono al token di autenticazione restituito ad AccessEnabler. Pertanto l’ID dispositivo è associato al token di autenticazione. Durante il flusso di autorizzazione, AccessEnabler invia nuovamente l&#39;ID dispositivo in modo chiaro, insieme al token di autenticazione. In caso di errore del processo di convalida si verifica automaticamente un errore dei flussi di lavoro di autenticazione/autorizzazione. I server di autenticazione Primetime applicano la chiave privata all&#39;ID dispositivo e la confrontano con il valore nel token di autenticazione. Se non corrispondono, il flusso di adesione non riesce.

 

**Nota relativa al binding dei dispositivi in AccessEnabler 1.7.5:** A partire da AccessEnabler 1.7.5, si verifica una modifica nella modalità di calcolo dell&#39;ID dispositivo per fornire informazioni di individualizzazione per un dispositivo iOS. Questa modifica riflette un cambiamento in iOS 7: Da iOS 7, Apple non fornisce più l’indirizzo MAC WiFi come opzione di tracciamento, a favore del suo identificatore per gli inserzionisti (IDFA). Poiché le informazioni di personalizzazione per un’app in esecuzione su iOS 7 si basano sull’identificatore IDFA e tali informazioni sono incorporate nei token del flusso di adesione, ciò significa che ci sono una serie di possibili effetti diversi sull’esperienza utente che risultano da questa modifica. I diversi effetti possibili si basano sulla versione di iOS che l&#39;utente sta aggiornando, combinata con la versione di AccessEnabler da cui il programmatore sta effettuando l&#39;aggiornamento. Per informazioni dettagliate su questa modifica, consulta le note sulla versione incluse in AccessEnabler SDK 1.7.5.

<!--
## Related Information {#related}


- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
