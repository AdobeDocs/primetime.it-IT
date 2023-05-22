---
title: Segnalazione errori
description: Segnalazione errori
exl-id: a52bd2cf-c712-40a2-a25e-7d9560b46ba6
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# Segnalazione errori {#error-reporting}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica {#overview}

La segnalazione degli errori nell’autenticazione di Adobe Primetime è attualmente implementata in due modi diversi:

* **Segnalazione avanzata degli errori** L’implementatore registra un callback di errore in caso di [SDK JavaScript per AccessEnabler](#accessenabler-javascript-sdk) o implementa un metodo di interfaccia denominato &quot;`status`&quot; in caso di [SDK di AccessEnabler iOS/tvOS](#accessenabler-ios-tvos-sdk) e [SDK per AccessEnabler Android](#accessenabler-android-sdk), per ricevere la segnalazione avanzata degli errori. Gli errori sono suddivisi in **Informazioni**, **Avvertenza**, e **Errore** tipi. Questo sistema di reporting è **asincrono**, in quanto **non c&#39;è garanzia dell&#39;ordine in cui verranno attivati più errori**.  Per informazioni dettagliate sul sistema avanzato di segnalazione degli errori, vedi [Segnalazione avanzata degli errori](#advanced-error-reporting) sezione.

* **Segnalazione errori originale -** Un sistema di reporting statico in cui i messaggi di errore vengono trasmessi a funzioni di callback specifiche quando determinate richieste hanno esito negativo. Gli errori sono raggruppati in tipi generici, di autenticazione e di autorizzazione. Per un elenco degli errori segnalati nel sistema originale, vedere [Segnalazione errori originale](#original-error-reporting) sezione.


## Segnalazione avanzata degli errori {#advanced-error-reporting}

* [SDK JavaScript per AccessEnabler](#accessenabler-javascript-sdk)
* [SDK di AccessEnabler iOS/tvOS](#accessenabler-ios-tvos-sdk)
* [SDK per AccessEnabler Android](#accessenabler-android-sdk)
* [SDK di AccessEnabler FireOS](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>Il vecchio [Segnalazione errori originale](#original-error-reporting) L’API continuerà a funzionare come in precedenza, ma la funzionalità della funzionalità di segnalazione avanzata degli errori non verrà interrotta, ma la funzionalità di segnalazione originale degli errori NON riceverà più aggiornamenti. Tutti i nuovi errori e aggiornamenti verranno eseguiti dal sistema di segnalazione errori avanzato.

### SDK JavaScript per AccessEnabler {#accessenabler-javascript-sdk}

Il nuovo sistema di segnalazione degli errori rimane facoltativo, pertanto l’implementatore può registrare esplicitamente un callback del gestore degli errori per ricevere segnalazioni avanzate degli errori. Il sistema include la possibilità di registrare e annullare la registrazione di più callback di errore in modo dinamico. Inoltre, è possibile registrare qualsiasi nuovo callback di errore non appena viene caricato l’SDK JavaScript di AccessEnabler, senza dover eseguire altre inizializzazioni (prima della chiamata `setRequestor()`), il che significa che puoi ricevere report avanzati sugli errori di inizializzazione e configurazione.


#### Implementazione {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


La funzione di callback del gestore degli errori riceverà un singolo oggetto (una mappa) con la seguente struttura:

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

### 1. Legare {#bind}

**`.bind(eventType:String, handlerName:String):void`**

Collega un gestore per un evento.

**`eventType`** - SOLO il &quot;`errorEvent`Il valore &quot; genera nell’SDK JavaScript di AccessEnabler l’attivazione di callback di report di errori avanzati.

**`handlerName`** - una stringa che specifica il nome della funzione di gestione degli errori.\
 

Entrambi i parametri di associazione devono utilizzare solo caratteri del seguente set: `[0-9a-zA-Z][-._a-zA-Z0-9]`I parametri devono iniziare con un numero o una lettera e possono quindi includere solo trattini, punti, trattini bassi e caratteri alfanumerici.  Inoltre, i parametri non possono superare i 1024 caratteri.  

**Esempio** di gestori di errori di associazione:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

A causa di limitazioni tecniche, non è possibile associare una chiusura o una funzione anonima. È necessario specificare il nome del metodo nel secondo parametro.

 
### 2. Separa {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

Rimuove un gestore eventi precedentemente associato.

**`eventType`** - SOLO &quot;`errorEvent`Il valore &#39; determina l&#39;attivazione da parte dell&#39;SDK JavaScript di AccessEnabler di callback di report di errori avanzati.

**`handlerName`** - una stringa che specifica il nome della funzione del gestore errori, se null o mancano tutti i gestori associati per il `eventType` verrà rimosso.

Entrambi i parametri di associazione devono utilizzare solo caratteri del seguente set: `[0-9a-zA-Z][-._a-zA-Z0-9]`I parametri devono iniziare con un numero o una lettera e possono quindi includere solo trattini, punti, trattini bassi e caratteri alfanumerici.  Inoltre, i parametri non possono superare i 1024 caratteri.  

**Esempio** di rimozione di un singolo gestore degli errori:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**Esempio** rimozione di tutti i gestori errori:

`accessEnabler.unbind('errorEvent');`


### SDK di AccessEnabler iOS/tvOS {#accessenabler-ios-tvos-sdk}

Il nuovo sistema di segnalazione degli errori è obbligatorio, pertanto l’implementatore deve conformarsi esplicitamente al nuovo protocollo &quot;EntitlementStatus&quot; dell’Obiettivo C. Questo nuovo approccio consente ai programmatori di ricevere report avanzati sugli errori.

#### Implementazione {#accessenab-ios-tvossdk-imp}

Un implementatore deve conformarsi a quanto segue **EntitlementStatus** protocollo:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

Il tuo **stato** la funzione riceverà un singolo oggetto (un `NSDictionary`) con la seguente struttura:

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


### SDK per AccessEnabler Android {#accessenabler-android-sdk}

Il nuovo sistema di segnalazione degli errori è obbligatorio, perché l’implementatore deve essere esplicitamente conforme al `IAccessEnablerDelegate` protocollo definito dall&#39;interfaccia. Questo nuovo approccio consente ai programmatori di ricevere report avanzati sugli errori.

#### Implementazione {#access-enablr-androidsdk-imp}

Un implementatore deve gestire il nuovo `status` metodo dall’interfaccia`IAccessEnablerDelegate`. Il **`status`** la funzione riceverà un singolo **`AdvancedStatus`** oggetto con il seguente modello:

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

### SDK di AccessEnabler FireOS {#accessenabler-fireos-sdk}


Il nuovo sistema di segnalazione degli errori è obbligatorio, perché l’implementatore deve essere esplicitamente conforme al `IAccessEnablerDelegate` protocollo definito dall&#39;interfaccia. Questo nuovo approccio consente ai programmatori di ricevere report avanzati sugli errori.

#### Implementazione {#access-enab-fireos-sdk-}

Un implementatore deve gestire il nuovo `status`metodo dall’interfaccia`IAccessEnablerDelegate`. Il **`status`** la funzione riceverà un singolo **`AdvancedStatus`** oggetto con il seguente modello:

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

## Riferimento codici di errore avanzati {#advanced-error-codes-reference}

La tabella seguente elenca e descrive i codici di errore esposti dalla nuova API di errore, insieme alle azioni suggerite da intraprendere per correggerli:

| ID | Livello | Descrizione | Azioni sviluppatore | Azioni utente | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL&amp; AAPL_ERROR | Errore | Errore SSO Apple generico | L’errore contiene un campo dei dettagli con l’errore VSA originale. | n/d | n/d | Sì | n/d |
| VSA203 | Info | L’utente ha deciso di uscire dall’applicazione mentre si verificava l’autenticazione a seguito di un accesso tramite l’SSO della piattaforma. | Indica/richiedi all&#39;utente di disconnettersi esplicitamente da Impostazioni -> Account -> Provider TV su tvOS. <br><br> Indica/richiede all’utente di disconnettersi esplicitamente da Impostazioni -> Provider TV su iOS/iPadOS. | Esci esplicitamente da Impostazioni -> Account -> Provider TV su tvOS. <br> <br> Esci esplicitamente da Impostazioni -> Provider TV su iOS/iPadOS | n/d | Sì | n/d |
| VSA404 | Info | L&#39;autorizzazione per l&#39;account sottoscrittore video dell&#39;applicazione non è determinata. | Incentivare gli utenti che rifiutano di concedere l&#39;autorizzazione per accedere alle informazioni sull&#39;abbonamento spiegando i vantaggi dell&#39;esperienza utente Single Sign-On (SSO). | L’utente può modificare la propria decisione andando nelle impostazioni dell’applicazione (accesso al provider TV) o nella sezione da Impostazioni -> Provider TV su iOS/iPadOS o Impostazioni -> Account -> Provider TV su tvOS. | n/d | Sì | n/d |
| VSA503 | Info | Richiesta metadati dell&#39;account del sottoscrittore video dell&#39;applicazione non riuscita. | L’endpoint MVPD non risponde. L’applicazione potrebbe eseguire il fallback a un flusso di autenticazione regolare. | n/d | n/d | Sì | n/d |
| 500 | Errore | Errore interno | Utilizza AccessEnablerDebug ed esamina i registri di debug (output console.log) per determinare cosa è andato storto. | n/d | Sì | Sì | n/d |
| SEC403 | Errore | Errore di sicurezza del dominio. Il richiedente utilizza un dominio non valido. Tutti i domini utilizzati da un particolare ID richiedente devono essere inseriti nella whitelist per Adobe. | - Carica AccessEnabler solo dall&#39;elenco dei domini consentiti <br> <br> - Contatta l’Adobe per gestire la whitelist del dominio per l’ID richiedente utilizzato <br> <br> - iOS: verifica di utilizzare il certificato corretto e che la firma sia stata creata correttamente | n/d | n/d | Sì | n/d |
| SEC412 | Avvertenza | [ Disponibile nella versione 2.5 ] ID dispositivo non corrispondente. Questo può accadere ogni volta che la piattaforma sottostante cambia il proprio ID dispositivo. In questo caso, i token esistenti verranno cancellati e l’utente non verrà più autenticato. Tieni presente che ciò accade legittimamente quando l’utente utilizza l’SDK JS e sta utilizzando roaming (su JS l’IP client fa parte dell’ID dispositivo). In caso contrario, potrebbe essere un’indicazione di un tentativo di frode, un tentativo di copiare token da un dispositivo diverso. | - Monitora il numero di avvisi. Se il picco non ha un motivo apparente (nessun aggiornamento recente del browser; nuovi sistemi operativi), potrebbe indicare tentativi di frode.  <br> <br>- Facoltativamente, informare l&#39;utente che deve effettuare di nuovo l&#39;accesso. | Accedi di nuovo. | Sì | Sì | Sì da 3.2 |
| SEC420 | Errore | Errore di sicurezza HTTP durante la comunicazione con i server di autenticazione di Adobe Primetime. Questo errore si verifica in genere quando sono presenti spoofing o proxy. | - Carica `[https://]{SP_FQDN\}` nel browser e accettare manualmente i certificati SSL, ad esempio, **https://api.auth.adobe.com** o **https://api.auth-staging.adobe.com** <br> <br>- Contrassegna i certificati proxy come attendibili | Se questo accade per un utente normale, è un&#39;indicazione di un possibile attacco man-in-the-middle! | Sì | Sì | Sì da 3.2 |
| CFG100 | Avvertenza | Data/ora/fuso orario del computer client non impostato correttamente. Questo potrebbe causare errori di autenticazione/autorizzazione. | - Informa l&#39;utente per impostare l&#39;ora corretta. <br> <br> Adottare misure per evitare flussi di diritti, poiché probabilmente non riusciranno. | Impostare la data/ora corretta. | Sì | Sì | Sì da 3.2 |
| CFG400 | Errore | È stato fornito un ID richiedente non valido. | Lo sviluppatore DEVE specificare un ID richiedente valido. | n/d | Sì | Sì | Sì da 3.2 |
| CFG404 | Errore | Impossibile trovare i server di autenticazione Adobe Primetime. Ciò può accadere in 3 istanze: <br><br> - Lo sviluppatore dispone di uno spoofing non valido. <br><br> -L’utente ha problemi di rete e non può raggiungere i domini di autenticazione di Adobe Primetime. <br><br> -I server di autenticazione di Adobe Primetime non sono configurati correttamente. <br><br>  **Nota:** Su Firefox, viene visualizzato CFG400 invece di CFG404 (limitazione del browser) | - Controllare la falsificazione. <br><br> -Controllare le impostazioni di rete/DNS. <br><br> -Informa Adobe. | Verificare le impostazioni di rete/DNS. | Sì | Sì | Sì da 3.2 |
| CFG410 | Errore | AccessEnabler è troppo vecchio. | Informa l’utente per cancellare le cache. | Cancella la cache del browser. | Sì | n/d | Sì da 3.2 |
| CFG5xx | Errore | Si sono verificati errori interni nei server di autenticazione di Adobe Primetime. xx può essere un numero qualsiasi. | : informa l’utente della non disponibilità dell’autenticazione di Adobe Primetime. <br><br> - Ignora l&#39;autenticazione Adobe Primetime. <br> <br> - Adobe informativo. | Riprova più tardi. | Sì | Sì | Sì da 3.2 |
| N000 | Info | Utente non autenticato. | n/d | Accedi. | Sì | Sì | Sì da 3.2 |
| N001 | Info | Tentativo di autenticazione passiva avviato in background. Ciò si verificherà per gli MVPD configurati con &quot;Autenticazione per richiedente&quot;. Anche se si spera che l’utente venga autenticato automaticamente, questo comporta una penalizzazione delle prestazioni al momento dell’inizializzazione. | Facoltativamente, informa l’utente, o presenta l’interfaccia utente che lo avvisa, che &quot;il lavoro è in corso&quot;. | Aspetta. | Sì | Sì | Sì da 3.2 |
| N003 | Info | L&#39;utente seleziona l&#39;opzione &quot;Altro provider TV&quot; dal selettore MVPD di Apple. | Il *displayProviderDialog* verrà chiamato il callback e l’applicazione potrebbe tornare al flusso di autenticazione normale. | Seleziona MVPD normale e continua con la schermata di accesso. | n/d | Sì | n/d |
| N004 | Info | L&#39;utente seleziona un provider TV non supportato dal richiedente corrente. | Il *displayProviderDialog* verrà chiamato il callback e l’applicazione potrebbe tornare al flusso di autenticazione normale. | Seleziona MVPD normale e continua con la schermata di accesso. | n/d | Sì | n/d |
| N005 | Info | Il selettore MVPD è stato annullato. | n/d | n/d | Sì | Sì | Sì da 3.2 |
| N010 | Avvertenza | L&#39;utente è stato autenticato mentre era in vigore la regola di degradazione authentication-all per l&#39;MVPD selezionato. | Facoltativamente, informare l&#39;utente che sta ottenendo l&#39;accesso gratuito &quot;gratuito&quot; a causa di difficoltà MVPD. | n/d | Sì | Sì | Sì da 3.2 |
| N011 | Info | L&#39;utente è stato autenticato tramite TempPass. | - Informare l&#39;utente. <br> <br> - Facoltativamente presentare un elenco di MVPD regolari. | Facoltativamente, accedi con il tuo MVPD regolare. | Sì | Sì | Sì da 3.2 |
| N111 | Avvertenza | TempPass scaduto. | - Informare l&#39;utente. <br> <br> - Presentare un elenco di MVPD regolari. <br> <br> - Nasconde l&#39;opzione TempPass. | Accedi con il tuo MVPD standard. | Sì | Sì | Sì da 3.2 |
| N130 | Errore | **Token di autenticazione non trovato nella sessione.**  Ciò può essere dovuto a uno dei seguenti fattori: <br> <br> 1. Il browser ha i cookie (di terze parti) disabilitati (non applicabile per AccessEnabler JavaScript SDK versione 4.x) <br> <br> 2. Il browser ha abilitato l’opzione Impedisci il rilevamento intersito (Safari 11+) <br> <br> 3. Sessione scaduta <br> <br> 4. Il programmatore chiama le API di autenticazione con una successione errata <br> <br> NOTA: questo codice di errore non è disponibile per i flussi di autenticazione di reindirizzamento a pagina intera. | 1. Richiedere all’utente di abilitare i cookie (di terze parti) <br> <br> 2. Richiedi all&#39;utente di disattivare il tracciamento intersito <br> <br> 3. Richiedi all&#39;utente di ripetere l&#39;autenticazione <br> <br> 4. Chiamare le API nell’ordine corretto | 1. Abilitare i cookie (di terze parti) <br> <br> 2. Disattiva il tracciamento intersito <br> <br> 3. Ripeti autenticazione <br> <br> 4. N/D | Sì | Sì | Sì da 3.2 |
| N500 | Errore | Errore interno. <br> <br> Nota: questo è l’errore originale del sistema &quot;Errore di autenticazione generico&quot; e &quot;Errore di autenticazione interna&quot;. Questo errore verrà gradualmente eliminato. | Utilizza AccessEnablerDebug ed esamina i registri di debug (output console.log) per determinare cosa è andato storto. | n/d | Sì | Sì | n/d |
| R401 | Errore | Errore durante il tentativo di ottenere un token di accesso. <br> <br> Nota: si tratta di un errore irreversibile. Informare l&#39;utente che l&#39;applicazione non è disponibile. | - iOS: controlla l’informativa software e gli schemi personalizzati nell’applicazione. <br> <br> - JavaScript: controlla l’istruzione software nell’applicazione del sito web. <br> <br> Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile | n/d | Sì dalla versione 4.0 | Sì dalla versione 3.0 | Sì da 3.2 |
| R400 | Errore | Applicazione non registrata. Dichiarazione software non valida o revocata. <br> <br> Nota: si tratta di un errore irreversibile. Informare l&#39;utente che l&#39;applicazione non è disponibile. | - iOS: controlla l’informativa software e gli schemi personalizzati nell’applicazione. <br> <br> - JavaScript: controlla l’istruzione software nell’applicazione del sito web. <br> <br> Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile | n/d | Sì dalla versione 4.0 | Sì dalla versione 3.0 | Sì da 3.2 |
| REG500 | Errore | Impossibile recuperare il codice di registrazione dal server. <br> <br> Nota: si tratta di un errore irreversibile. Informare l&#39;utente che l&#39;applicazione non è disponibile. | Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile. | n/d | Sì dalla versione 4.0 | Sì dalla versione 3.0 | Sì da 3.2 |
| REGCODE | Completato | L’applicazione ha chiamato l’API setSelectedProvider sulla piattaforma tvOS. | Indica/richiede all&#39;utente di utilizzare un secondo dispositivo (schermata) per accedere utilizzando il codice di registrazione fornito. | Utilizza il codice regcode su un secondo dispositivo (schermata) per avviare l’autenticazione. | n/d | Sì Solo per tvOS | n/d |
| Z010 | Avvertenza | L&#39;utente è stato autorizzato mentre era in vigore la regola di degradazione authentication-all o authorize-all per l&#39;MVPD selezionato. | Facoltativamente, informare l&#39;utente che sta ottenendo l&#39;accesso gratuito &quot;gratuito&quot; a causa di difficoltà MVPD. | n/d | Sì | Sì | Sì da 3.2 |
| Z011 | Info | L&#39;utente è stato autorizzato tramite TempPass | Facoltativamente, informare l&#39;utente | n/d | Sì | Sì | Sì da 3.2 |
| Z100 | Errore | Autorizzazione non riuscita perché l’utente non dispone di un abbonamento per la risorsa richiesta o per altri motivi derivanti dall’MVPD, ad esempio perché il video non corrisponde alle impostazioni di Controllo genitori per l’account utente | - Non consentire la riproduzione. <br> <br> - Informare l&#39;utente. <br> <br> - La chiave &quot;message&quot; nel messaggio di errore PUÒ contenere un messaggio più dettagliato fornito dall&#39;MVPD. | n/d | Sì | Sì | Sì da 3.2 |
| Z110 | Errore | Autorizzazione negata a causa di ripetuti rifiuti MVPD. Possibile tentativo di frode o DOS. | - Non consentire la riproduzione. <br> <br> - Informare l&#39;utente. | n/d | Sì | Sì | Sì da 3.2 |
| Z120 | Errore | Autorizzazione negata per motivi tecnici nella comunicazione con l&#39;MVPD. Possibile errore di rete. | - Non consentire la riproduzione. <br> <br> - Informare l&#39;utente che l&#39;MVPD ha incontrato difficoltà e riprovare più tardi. | Riprova più tardi. | Sì | Sì | Sì da 3.2 |
| Z130 | Errore | Autorizzazione negata perché è stata utilizzata una risorsa non valida o non valida. | Controlla la stringa di risorsa e correggila. In genere questo errore è dovuto a un MRSS non valido o all&#39;utilizzo di una stringa semplice al posto di MRSS. | n/d | Sì | Sì | Sì da 3.2 |
| Z169 | Errore | Autorizzazione negata perché è stata applicata la regola di degradazione authzNone per la risorsa specificata. | Informa l’utente | n/d | Sì | Sì | Sì da 3.2 |
| Z500 | Errore | Errore interno. <br> <br>  Nota: si tratta dei precedenti &quot;Errore di autenticazione generica&quot; e &quot;Errore di autenticazione interna&quot;. Questo errore verrà gradualmente eliminato. | Utilizza AccessEnablerDebug ed esamina i registri di debug (output console.log) per determinare cosa è andato storto. | n/d | Sì | Sì | Sì da 3.2 |
| P100 | Errore | Preautorizzazione non riuscita. Molto probabilmente ciò è dovuto alla richiesta di autorizzazione per troppe risorse. | - NON utilizzare un numero di risorse superiore a quello massimo consentito. <br> <br> - Contatta il supporto per l’autenticazione di Adobe Primetime per trovare/impostare il numero massimo di risorse consentite. | n/d | Sì dalla versione 3.0 | Sì | Sì da 3.2 |
| IS2XX | Errore | Questi codici di errore vengono restituiti quando i dati di risposta dell&#39;endpoint del server di personalizzazione hanno un formato non valido o mancano le informazioni di personalizzazione richieste. | Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile | n/d | Sì dalla versione 3.0 | n/d | n/d |
| IS4XX | Errore | Questi codici di errore vengono restituiti in caso di errore dell’endpoint del server di individualizzazione 4XX: è il codice di stato HTTP della risposta. | Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile | n/d | Sì dalla versione 3.0 | n/d | n/d |
| IS5XX | Errore | Questi codici di errore vengono restituiti in caso di errore dell’endpoint del server di individualizzazione 5XX: è il codice di stato HTTP della risposta. | Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile | n/d | Sì dalla versione 3.0 | n/d | n/d |
| IS0 | Errore | Questo codice viene restituito quando l&#39;endpoint del server di individuazione non risponde affatto, pertanto la connessione è scaduta | Apri un ticket utilizzando Zendesk e informa l’utente che il sistema è temporaneamente non disponibile | n/d | Sì dalla versione 3.0 | n/d | n/d |
| LS011 | Avvertenza | AccessEnabler utilizza un&#39;archiviazione volatile a causa di problemi LSO/LocalStorage e di problemi di WebStorage (o di indisponibilità). <br> <br> L&#39;autenticazione/autorizzazione non persiste oltre la pagina corrente. A ogni caricamento di pagina l’utente dovrà eseguire l’autenticazione. I TTL configurati non vengono applicati nei diversi ricaricamenti delle pagine. | - Informare l&#39;utente delle limitazioni. <br> <br> - Informare l&#39;utente su come aumentare lo spazio di archiviazione disponibile. <br> <br> - In alternativa, disconnettersi per cancellare l&#39;archiviazione. | - Aumentare lo storage. <br> <br> - Disconnettersi per cancellare l&#39;archiviazione. | Sì | n/d | n/d |

<br>

## Segnalazione errori originale {#original-error-reporting}

Questa sezione descrive il sistema di segnalazione degli errori originale e i codici di errore originali. Nel sistema di segnalazione degli errori originale, AccessEnabler trasmette gli errori alle due funzioni di callback seguenti: `setAuthenticationStatus()` dopo una chiamata a `checkAuthentication()`; `tokenRequestFailed()`, dopo il guasto di una chiamata a `checkAuthorization()` o `getAuthorization()`.

La segnalazione degli errori originale e le API di stato continuano a funzionare esattamente come prima. Tuttavia, andando avanti le API di segnalazione errori originali non verranno aggiornate. Tutte le nuove segnalazioni di errori e gli aggiornamenti sui vecchi errori verranno rispecchiati SOLO nel nuovo [Sistema di Segnalazione avanzata degli errori](#advanced-error-reporting).


Per esempi di utilizzo del sistema di segnalazione errori originale, vedere [Riferimento API per JavaScript](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) e [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) funzioni, [Riferimento API per iOS/tvOS](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)e [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Riferimento API per Android](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) e [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### Codici di errore del callback originale {#original-callback-error-codes}

| **Errori generici** |  |
|---|---|
| Errore interno | Si è verificato un errore di sistema durante il tentativo di elaborare la richiesta. |
| Errore provider non selezionato | Si verifica in seguito all&#39;annullamento del cliente nella finestra di dialogo di selezione del provider. |
| Errore provider non disponibile | Si verifica quando non è disponibile alcun provider. |
|  |  |
| **Errori di autenticazione** |  |
| Errore di autenticazione generica | Restituito quando il motivo non è noto o non può essere pubblicato. |
| Errore di autenticazione interna | Si è verificato un errore di sistema durante il tentativo di autenticazione. |
| Errore utente non autenticato | Utente non autenticato. |
|  |  |
| **Errori di autorizzazione** |  |
| Errore di autorizzazione generica | Restituito quando il motivo non è noto o non può essere pubblicato. |
| Errore di autorizzazione interna | Si è verificato un errore di sistema durante il tentativo di autorizzazione. |
| Errore utente non autorizzato | Il cliente non è autorizzato a visualizzare il contenuto richiesto. |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->
