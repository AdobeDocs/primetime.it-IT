---
title: Segnalazione errori
description: Segnalazione errori
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# Segnalazione errori {#error-reporting}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica {#overview}

La generazione di rapporti sugli errori nell’autenticazione Adobe Primetime è attualmente implementata in due modi diversi:

* **Generazione avanzata di rapporti sugli errori** L’implementatore registra un callback di errore nel caso in cui [SDK JavaScript per AccessEnabler](#accessenabler-javascript-sdk) o implementa un metodo Interface denominato &quot;`status`&quot; nel caso di [SDK di AccessEnabler per iOS/tvOS](#accessenabler-ios-tvos-sdk) e [SDK per Android di AccessEnabler](#accessenabler-android-sdk), per ricevere la segnalazione avanzata degli errori. Gli errori sono suddivisi in categorie **Informazioni**, **Avviso** e **Errore** tipi. Questo sistema di segnalazione è **asincrono**, in quanto **non vi è alcuna garanzia dell&#39;ordine in cui verranno attivati più errori**.  Per informazioni dettagliate sul sistema avanzato di segnalazione degli errori, vedi [Generazione avanzata di rapporti sugli errori](#advanced-error-reporting) sezione .

* **Segnalazione errori originali -** Un sistema di reporting statico in cui i messaggi di errore vengono passati a specifiche funzioni di callback quando richieste specifiche non riescono. Gli errori sono raggruppati in tipi generici, di autenticazione e di autorizzazione. Per l&#39;elenco degli errori segnalati nel sistema originale, vedi [Segnalazione errori originale](#original-error-reporting) sezione .


## Generazione avanzata di rapporti sugli errori {#advanced-error-reporting}

* [SDK JavaScript per AccessEnabler](#accessenabler-javascript-sdk)
* [SDK di AccessEnabler per iOS/tvOS](#accessenabler-ios-tvos-sdk)
* [SDK per Android di AccessEnabler](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>I vecchi [Segnalazione errori originale](#original-error-reporting) L’API continuerà a funzionare come in precedenza, la generazione di rapporti sugli errori avanzati non interrompe la funzionalità, ma la segnalazione degli errori originali NON riceverà più aggiornamenti. Tutti i nuovi errori e aggiornamenti si verificheranno al sistema avanzato di segnalazione degli errori.

### SDK JavaScript per AccessEnabler {#accessenabler-javascript-sdk}

Il nuovo sistema di segnalazione degli errori viene lasciato opzionale, pertanto l’implementatore può registrare esplicitamente un callback del gestore degli errori per ricevere report di errore avanzati. Il sistema include la possibilità di registrare e annullare la registrazione dinamica di più callback di errore. Inoltre, è possibile registrare qualsiasi nuovo callback di errore non appena viene caricato l&#39;SDK JavaScript di AccessEnabler, senza la necessità di eseguire alcuna altra inizializzazione (prima di richiamare `setRequestor()`), ovvero puoi ricevere report avanzati sugli errori di inizializzazione e configurazione.


#### Implementazione {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


La funzione di callback del gestore di errori riceverà un singolo oggetto (una mappa) con la seguente struttura:

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1. Associazione {#bind}

**`.bind(eventType:String, handlerName:String):void`**

Associa un gestore per un evento.

**`eventType`** - SOLO &quot;`errorEvent`&quot; restituisce come risultato l&#39;attivazione di callback di report di errore avanzati da parte dell&#39;SDK JavaScript di AccessEnabler.

**`handlerName`** - una stringa che specifica il nome della funzione del gestore errori.\
 

Entrambi i parametri di binding devono utilizzare solo caratteri del set seguente: `[0-9a-zA-Z][-._a-zA-Z0-9]`; in altre parole, i parametri devono iniziare con un numero o una lettera e possono quindi includere solo trattini, periodi, caratteri di sottolineatura e caratteri alfanumerici.  Inoltre, i parametri non possono superare i 1024 caratteri.  

**Esempio** di gestori di errori di binding:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

A causa di limitazioni tecniche non è possibile eseguire il binding di una chiusura o di una funzione anonima. È necessario specificare il nome del metodo nel secondo parametro.

 
### 2. Separa {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

Rimuove un gestore eventi allegato in precedenza.

**`eventType`** - SOLO il`errorEvent`Il valore &#39; restituisce l&#39;attivazione dei callback dei report di errore avanzati da parte dell&#39;SDK JavaScript di AccessEnabler.

**`handlerName`** - una stringa che specifica il nome della funzione dell&#39;handler degli errori, se è nullo o se mancano tutti i gestori associati per l&#39;oggetto specificato `eventType` verrà rimosso.

Entrambi i parametri di binding devono utilizzare solo caratteri del set seguente: `[0-9a-zA-Z][-._a-zA-Z0-9]`; in altre parole, i parametri devono iniziare con un numero o una lettera e possono quindi includere solo trattini, periodi, caratteri di sottolineatura e caratteri alfanumerici.  Inoltre, i parametri non possono superare i 1024 caratteri.  

**Esempio** per rimuovere un singolo gestore di errori:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**Esempio** rimozione di tutti i gestori errori:

`accessEnabler.unbind('errorEvent');`


### SDK di AccessEnabler per iOS/tvOS {#accessenabler-ios-tvos-sdk}

Il nuovo sistema di segnalazione degli errori è obbligatorio, pertanto l’implementatore deve conformarsi esplicitamente al nuovo protocollo Objective-C &quot;EntitlementStatus&quot;. Questo nuovo approccio consente ai programmatori di ricevere una segnalazione avanzata degli errori.

#### Implementazione {#accessenab-ios-tvossdk-imp}

Un implementatore deve conformarsi ai seguenti requisiti **EntitlementStatus** protocollo:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

Le **status** riceverà un singolo oggetto (un `NSDictionary`) con la seguente struttura:

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. Dichiarazione**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. Implementazione**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### SDK per Android di AccessEnabler {#accessenabler-android-sdk}

Il nuovo sistema di segnalazione degli errori è obbligatorio, perché l’implementatore deve essere esplicitamente conforme al `IAccessEnablerDelegate` protocollo definito dall&#39;interfaccia. Questo nuovo approccio consente ai programmatori di ricevere una segnalazione avanzata degli errori.

#### Implementazione {#access-enablr-androidsdk-imp}

Un implementatore deve gestire il nuovo `status` dall&#39;interfaccia`IAccessEnablerDelegate`. La **`status`** riceverà un&#39;unica funzione **`AdvancedStatus`** oggetto con il seguente modello:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Esempio**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


Il nuovo sistema di segnalazione degli errori è obbligatorio, perché l’implementatore deve essere esplicitamente conforme al `IAccessEnablerDelegate` protocollo definito dall&#39;interfaccia. Questo nuovo approccio consente ai programmatori di ricevere una segnalazione avanzata degli errori.

#### Implementazione {#access-enab-fireos-sdk-}

Un implementatore deve gestire il nuovo `status`dall&#39;interfaccia`IAccessEnablerDelegate`. La **`status`** riceverà un&#39;unica funzione **`AdvancedStatus`** oggetto con il seguente modello:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Esempio**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## Riferimento per i codici di errore avanzati {#advanced-error-codes-reference}

La tabella seguente elenca e descrive i codici di errore esposti dalla nuova API di errore, insieme alle azioni suggerite da intraprendere per correggerli:

| ID | Livello | Descrizione | Azioni per sviluppatori | Azioni utente | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL&amp; AAPL_ERROR | Errore | Errore Apple SSO generico | L&#39;errore contiene un campo di dettagli con l&#39;errore VSA originale. | n/d | n/d | Sì | n/d |
| VSA203 | Info | L&#39;utente ha deciso di disconnettersi dall&#39;applicazione mentre si verificava l&#39;autenticazione a seguito di un accesso tramite la piattaforma SSO. | Chiedi/chiedi all&#39;utente di disconnettersi in modo esplicito da Impostazioni -> Account -> Provider TV su tvOS. <br><br> Chiedi/chiedi all&#39;utente di disconnettersi in modo esplicito da Settings -> TV Provider su iOS/iPadOS. | Disconnettiti in modo esplicito da Impostazioni -> Account -> Provider TV su tvOS. <br> <br> Disconnessione esplicita da Settings -> TV Provider su iOS/iPadOS | n/d | Sì | n/d |
| VSA404 | Info | Autorizzazione account utente con sottoscrizione video dell&#39;applicazione non determinata. | Incentivare gli utenti che rifiutano di concedere l’autorizzazione all’accesso alle informazioni di abbonamento spiegando i vantaggi dell’esperienza utente Single Sign-On (SSO). | L&#39;utente può cambiare la sua decisione andando alle impostazioni dell&#39;applicazione (accesso al provider TV) o alla sezione da Impostazioni -> Provider TV su iOS/iPadOS o Impostazioni -> Account -> Provider TV su tvOS. | n/d | Sì | n/d |
| VSA503 | Info | Richiesta dei metadati dell&#39;account del sottoscrittore video dell&#39;applicazione non riuscita. | L&#39;endpoint MVPD non risponde. L&#39;applicazione potrebbe fallback al flusso di autenticazione regolare. | n/d | n/d | Sì | n/d |
| 500 | Errore | Errore interno | Utilizza AccessEnablerDebug ed esamina i log di debug (output console.log) per determinare cosa è andato storto. | n/d | Sì | Sì | n/d |
| SEC403 | Errore | Errore di sicurezza del dominio. Il richiedente sta utilizzando un dominio non valido. Tutti i domini utilizzati da un particolare ID richiedente devono essere elencati nella whitelist di Adobe. | - Carica AccessEnabler solo dall&#39;elenco dei domini consentiti <br> <br> - Adobe di contatto per gestire la whitelist del dominio per l&#39;ID del richiedente utilizzato <br> <br> - iOS: verificare di utilizzare il certificato corretto e che la firma sia stata creata correttamente | n/d | n/d | Sì | n/d |
| SEC412 | Avviso | [ Disponibile nella versione 2.5 ] L&#39;ID dispositivo non corrisponde. Questo può accadere ogni volta che la piattaforma sottostante cambia il proprio ID dispositivo. In questo caso, i token esistenti verranno cancellati e l’utente non sarà più autenticato. Tieni presente che ciò accade legittimamente quando l’utente utilizza l’SDK JS e sta utilizzando in roaming (su JS l’IP client fa parte dell’ID dispositivo). In caso contrario, ciò potrebbe indicare un tentativo di frode - un tentativo di copiare i token da un dispositivo diverso. | - Monitorare il numero di avvisi. Se il picco non ha motivo apparente (nessun aggiornamento recente del browser; nuovi sistemi operativi) che potrebbero essere un indicatore dei tentativi di frode.  <br> <br>- In alternativa, informa l&#39;utente che deve effettuare di nuovo l&#39;accesso. | Accedi di nuovo. | Sì | Sì | Sì da 3.2 |
| SEC420 | Errore | Errore di sicurezza HTTP durante la comunicazione con i server di autenticazione Adobe Primetime. Questo errore si verifica in genere quando si verificano spoofing / proxy. | - Carico `[https://]{SP_FQDN\}` nel browser e accetta manualmente i certificati SSL, ad esempio: **https://api.auth.adobe.com** o **https://api.auth-staging.adobe.com** <br> <br>- Contrassegnare i certificati proxy come affidabili | Se questo si verifica per un utente normale, è un&#39;indicazione di un possibile attacco man-in-the-middle! | Sì | Sì | Sì da 3.2 |
| CFG100 | Avviso | La data/ora/fuso orario del computer client non è impostata correttamente. Questo porterà probabilmente a errori di autenticazione/autorizzazione. | - Informare l&#39;utente di impostare l&#39;ora corretta. <br> <br> Adottare misure per impedire i flussi di adesione, in quanto probabilmente avranno esito negativo. | Imposta la data/ora corretta. | Sì | Sì | Sì da 3.2 |
| CFG400 | Errore | È stato fornito un ID richiedente non valido. | Lo sviluppatore DEVE specificare un ID richiedente valido. | n/d | Sì | Sì | Sì da 3.2 |
| CFG404 | Errore | Impossibile trovare i server di autenticazione Adobe Primetime. Questo può accadere in 3 casi: <br><br> - Lo sviluppatore dispone di uno spoofing non valido. <br><br> - L’utente ha problemi di rete e non può raggiungere i domini di autenticazione di Adobe Primetime. <br><br> - I server di autenticazione Adobe Primetime non sono configurati correttamente. <br><br>  **Nota:** Su Firefox, CFG400 apparirà invece di CFG404 (limitazione browser) | - Controllare lo spoofing. <br><br> -Controllare le impostazioni di rete / DNS. <br><br> - Adobe di informazioni. | Controllare le impostazioni di rete/DNS. | Sì | Sì | Sì da 3.2 |
| CFG410 | Errore | AccessEnabler è troppo vecchio. | Informare l&#39;utente per cancellare le cache. | Cancella la cache del browser. | Sì | n/d | Sì da 3.2 |
| CFG5xx | Errore | Errori interni ai server di autenticazione Adobe Primetime. xx può essere un qualsiasi numero. | - Informare l&#39;utente dell&#39;indisponibilità dell&#39;autenticazione Adobe Primetime. <br><br> - Salto dell’autenticazione Adobe Primetime. <br> <br> - Informare l&#39;Adobe. | Provi più tardi. | Sì | Sì | Sì da 3.2 |
| N000 | Info | Utente non autenticato. | n/d | Accedi. | Sì | Sì | Sì da 3.2 |
| N001 | Info | È stato avviato un tentativo di autenticazione passiva in background. Questo accade per gli MVPD configurati con &quot;Authentication Per Requestor&quot;. Se si spera che l’utente venga autenticato automaticamente, ciò comporta una sanzione delle prestazioni in caso di inizializzazione. | Se necessario, informa l’utente o l’interfaccia utente attuale che avvisa l’utente che &quot;il lavoro è in corso&quot;. | Aspetta. | Sì | Sì | Sì da 3.2 |
| N003 | Info | L&#39;utente seleziona l&#39;opzione &quot;Altro provider TV&quot; dal selettore MVPD di Apple. | La *displayProviderDialog* viene chiamato il callback e l&#39;applicazione può fare riferimento al flusso di autenticazione regolare. | Seleziona MVPD normale e continua con la schermata di accesso. | n/d | Sì | n/d |
| N004 | Info | L&#39;utente seleziona un provider TV non supportato dal richiedente corrente. | La *displayProviderDialog* viene chiamato il callback e l&#39;applicazione può fare riferimento al flusso di autenticazione regolare. | Seleziona MVPD normale e continua con la schermata di accesso. | n/d | Sì | n/d |
| N005 | Info | Il selettore MVPD è stato annullato. | n/d | n/d | Sì | Sì | Sì da 3.2 |
| N010 | Avviso | L&#39;utente è stato autenticato mentre era in vigore la regola di degradazione autenticate-all per l&#39;MVPD selezionato. | Facoltativamente informare l&#39;utente che sta ottenendo &quot;gratuito&quot; accesso a causa di difficoltà MVPD. | n/d | Sì | Sì | Sì da 3.2 |
| N011 | Info | L&#39;utente è stato autenticato tramite TempPass. | - Informare l&#39;utente. <br> <br> - Presentare facoltativamente un elenco di MVPD regolari. | Se necessario, effettua il login con il tuo MVPD normale. | Sì | Sì | Sì da 3.2 |
| N111 | Avviso | TempPass scaduto. | - Informare l&#39;utente. <br> <br> - Presentare un elenco degli MVPD regolari. <br> <br> - Nascondi l&#39;opzione TempPass. | Accedi con il tuo MVPD normale. | Sì | Sì | Sì da 3.2 |
| N130 | Errore | **Token di autenticazione non trovato nella sessione.**  Ciò può essere dovuto a uno dei seguenti fattori: <br> <br> 1. Il browser ha i cookie (di terze parti) disabilitati (non applicabile per AccessEnabler JavaScript SDK versione 4.x) <br> <br> 2. Il browser ha l’opzione Impedisci il tracciamento intersito abilitato (Safari 11+) <br> <br> 3. Sessione scaduta <br> <br> 4. Il programmatore chiama le API di autenticazione in successione errata <br> <br> NOTA: Questo codice di errore non è disponibile per i flussi di autenticazione di reindirizzamento a pagina intera. | 1. Richiedi all’utente di abilitare i cookie (di terze parti) <br> <br> 2. Promt user to disable cross-site tracking <br> <br> 3. Richiedi all&#39;utente di eseguire nuovamente l&#39;autenticazione <br> <br> 4. Chiama le API in ordine corretto | 1. Abilitare i cookie (di terze parti) <br> <br> 2. Disattiva il tracciamento tra siti <br> <br> 3. Ripetizione autenticazione <br> <br> 4. N/D | Sì | Sì | Sì da 3.2 |
| N500 | Errore | Errore interno. <br> <br> Nota: Si tratta dell&#39;errore originale del sistema di errore &quot;Errore di autenticazione generico&quot; e &quot;Errore di autenticazione interna&quot;. Questo errore verrà infine eliminato gradualmente. | Utilizza AccessEnablerDebug ed esamina i log di debug (output console.log) per determinare cosa è andato storto. | n/d | Sì | Sì | n/d |
| R401 | Errore | Errore durante il tentativo di ottenere un token di accesso. <br> <br> Nota: Errore irreversibile. Informare l&#39;utente che l&#39;applicazione non è disponibile. | - iOS: Controllare l&#39;istruzione software e gli schemi personalizzati nella vostra applicazione. <br> <br> - JavaScript: Controllare l&#39;istruzione software nell&#39;applicazione Web. <br> <br> Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile | n/d | Sì Da v4.0 | Sì Da v3.0 | Sì da 3.2 |
| R400 | Errore | Applicazione non registrata. Istruzione software non valida o revocata. <br> <br> Nota: Errore irreversibile. Informare l&#39;utente che l&#39;applicazione non è disponibile. | - iOS: Controllare l&#39;istruzione software e gli schemi personalizzati nella vostra applicazione. <br> <br> - JavaScript: Controllare l&#39;istruzione software nell&#39;applicazione Web. <br> <br> Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile | n/d | Sì Da v4.0 | Sì Da v3.0 | Sì da 3.2 |
| REG500 | Errore | Impossibile recuperare il codice di registrazione dal server. <br> <br> Nota: Errore irreversibile. Informare l&#39;utente che l&#39;applicazione non è disponibile. | Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile. | n/d | Sì Da v4.0 | Sì Da v3.0 | Sì da 3.2 |
| REGCODIFICA | Completato | L&#39;applicazione ha chiamato l&#39;API setSelectedProvider sulla piattaforma tvOS. | Informa/richiedi all&#39;utente di utilizzare un secondo dispositivo (schermo) per accedere utilizzando il codice di registrazione fornito. | Utilizza il regcode su un secondo dispositivo (schermo) per avviare l’autenticazione. | n/d | Sì Solo per tvOS | n/d |
| Z010 | Avviso | L&#39;utente è stato autorizzato mentre la regola di degrado di tutte le autorizzazioni o tutte le operazioni di autenticazione era in posizione per il MVPD selezionato. | Facoltativamente informare l&#39;utente che sta ottenendo &quot;gratuito&quot; accesso a causa di difficoltà MVPD. | n/d | Sì | Sì | Sì da 3.2 |
| Z011 | Info | Utente autorizzato tramite TempPass | Facoltativamente informare l&#39;utente | n/d | Sì | Sì | Sì da 3.2 |
| Z100 | Errore | Autorizzazione non riuscita perché l&#39;utente non dispone di un abbonamento per la risorsa richiesta o per altri motivi originati dall&#39;MVPD, ad esempio il video non corrisponde alle impostazioni di Controllo genitori per l&#39;account utente | - Non consentire la riproduzione. <br> <br> - Informare l&#39;utente. <br> <br> - La chiave &#39;message&#39; nel messaggio di errore POTREBBE contenere un messaggio più dettagliato fornito dall&#39;MVPD. | n/d | Sì | Sì | Sì da 3.2 |
| Z110 | Errore | Autorizzazione negata a causa di ripetuti rifiuti MVPD. Possibile tentativo di frode o DOS. | - Non consentire la riproduzione. <br> <br> - Informare l&#39;utente. | n/d | Sì | Sì | Sì da 3.2 |
| Z120 | Errore | Autorizzazione negata per motivi tecnici nella comunicazione con l&#39;MVPD. Possibile errore di rete. | - Non consentire la riproduzione. <br> <br> - Informare l&#39;utente che l&#39;MVPD ha avuto difficoltà e dovrebbero provare più tardi. | Provi più tardi. | Sì | Sì | Sì da 3.2 |
| Z130 | Errore | Autorizzazione negata perché è stata utilizzata una risorsa non valida o non valida. | Controlla la stringa della risorsa e correggilo. Generalmente questo errore è dovuto a un MRSS malformato o all&#39;uso di una stringa normale invece di MRSS. | n/d | Sì | Sì | Sì da 3.2 |
| Z169 | Errore | Autorizzazione negata perché la regola di degrado authzNone è stata applicata alla risorsa specificata. | Informare l&#39;utente | n/d | Sì | Sì | Sì da 3.2 |
| Z500 | Errore | Errore interno. <br> <br>  Nota: si tratta dell&#39;errore legacy &quot;Errore di autenticazione generico&quot; e &quot;Errore di autenticazione interna&quot;. Questo errore verrà infine eliminato gradualmente. | Utilizza AccessEnablerDebug ed esamina i log di debug (output console.log) per determinare cosa è andato storto. | n/d | Sì | Sì | Sì da 3.2 |
| P100 | Errore | Preautorizzazione non riuscita. Molto probabilmente ciò è dovuto alla richiesta di autorizzazione per troppe risorse. | - NON utilizzare più del numero massimo di risorse consentite. <br> <br> - Contatta il supporto per l’autenticazione di Adobe Primetime per trovare/impostare il numero massimo di risorse consentite. | n/d | Sì Da v3.0 | Sì | Sì da 3.2 |
| IS2XX | Errore | Questi codici di errore vengono restituiti quando i dati di risposta dell’endpoint del server di individualizzazione hanno un formato non valido o mancano le informazioni di individualizzazione richieste. | Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile | n/d | Sì Da v3.0 | n/d | n/d |
| IS4XX | Errore | Questi codici di errore vengono restituiti in caso di errore dell’endpoint server di individualizzazione 4XX - è il codice di stato HTTP della risposta. | Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile | n/d | Sì Da v3.0 | n/d | n/d |
| IS5XX | Errore | Questi codici di errore vengono restituiti in caso di errore 5XX dell&#39;endpoint del server di individualizzazione - è il codice di stato HTTP della risposta. | Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile | n/d | Sì Da v3.0 | n/d | n/d |
| IS0 | Errore | Questo codice viene restituito quando l&#39;endpoint del server di individualizzazione non ha risposto affatto, pertanto la connessione è scaduta | Apri un ticket utilizzando Zendesk e informa l&#39;utente che il sistema è temporaneamente non disponibile | n/d | Sì Da v3.0 | n/d | n/d |
| LS011 | Avviso | AccessEnabler sta utilizzando uno storage volatile a causa di problemi di LSO / LocalStorage e problemi di WebStorage (o indisponibilità). <br> <br> L&#39;autenticazione / autorizzazione non persiste oltre la pagina corrente. A causa di ogni caricamento di pagina, l’utente dovrà eseguire l’autenticazione. I TTL configurati non vengono applicati nei ricaricamenti delle pagine. | - Informare l&#39;utente delle limitazioni. <br> <br> - Informare l&#39;utente su come aumentare lo spazio di archiviazione disponibile. <br> <br> - In alternativa, effettuare il logout per cancellare lo storage. | - Aumentare lo storage. <br> <br> - Disconnessione per cancellare lo storage. | Sì | n/d | n/d |

<br>

## Segnalazione errori originale {#original-error-reporting}

Questa sezione descrive il sistema di segnalazione degli errori originale, insieme ai codici di errore originali. Nel sistema di segnalazione degli errori originale, AccessEnabler trasmette gli errori alle due funzioni di callback seguenti: `setAuthenticationStatus()` dopo una chiamata a `checkAuthentication()`; `tokenRequestFailed()`, dopo il fallimento di una chiamata a `checkAuthorization()` o `getAuthorization()`.

La segnalazione degli errori originali e le API di stato continuano a funzionare esattamente come prima. In futuro, tuttavia, le API di segnalazione degli errori originali non verranno aggiornate. Tutte le nuove segnalazioni di errori e gli aggiornamenti sui vecchi errori verranno riportati SOLO nella nuova [Sistema avanzato di segnalazione degli errori](#advanced-error-reporting).


Per esempi sull’utilizzo del sistema di segnalazione degli errori originale, consulta la sezione [Riferimento API JavaScript](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) e [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) funzioni, [Riferimento API di iOS/tvOS](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)e [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Riferimento API per Android](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) e [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### Codici errore callback originali {#original-callback-error-codes}

| **Errori generici** |  |
|---|---|
| Errore interno | Errore di sistema durante il tentativo di elaborare la richiesta. |
| Errore del provider non selezionato | Si verifica quando il cliente annulla nella finestra di dialogo di selezione del provider. |
| Errore del provider non disponibile | Si verifica quando non sono disponibili provider. |
|  |  |
| **Errori di autenticazione** |  |
| Errore di autenticazione generico | Restituito quando il motivo non è noto o non può essere pubblicato. |
| Errore di autenticazione interna | Errore di sistema durante il tentativo di autenticazione. |
| Errore utente non autenticato | Utente non autenticato. |
|  |  |
| **Errori di autorizzazione** |  |
| Errore di autorizzazione generico | Restituito quando il motivo non è noto o non può essere pubblicato. |
| Errore di autorizzazione interna | Errore di sistema durante il tentativo di autorizzazione. |
| Errore non autorizzato dell&#39;utente | Il cliente non è autorizzato a visualizzare il contenuto richiesto. |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->