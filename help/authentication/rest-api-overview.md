---
title: Panoramica API REST
description: Panoramica per le API rimanenti
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 0%

---


# Panoramica API REST {#rest-api-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica {#over}

L’API REST di autenticazione Adobe Primetime fornisce l’accesso diretto ai servizi di autenticazione e autorizzazione TV Everywhere (TVE). Questa API supporta due architetture principali: Dispositivi collegati o server (ad esempio console di gioco, Smart TV, set-top box, ecc.) applicazioni prive di funzionalità di navigazione web. 

 

### Server-to-server

Le soluzioni server-to-server coinvolgono applicazioni client programmatori che si integrano con i servizi programmatori che si connettono con i servizi di autenticazione Adobe Primetime per i flussi TVE. Questo approccio sposta la maggior parte dell’implementazione TVE dal client al server, dove è possibile creare e mantenere un singolo modulo di autorizzazione unificato. La principale responsabilità rimanente delle applicazioni client è la gestione di una visualizzazione web per l&#39;autenticazione degli utenti.

 

### Dispositivi collegati

Le app dei dispositivi collegati comunicano direttamente con l’autenticazione di Primetime tramite le API REST per eseguire la configurazione, la registrazione, i controlli dello stato di autenticazione e i flussi di autorizzazione, mentre per il flusso di autenticazione è necessaria un’app a seconda schermata (browser). Di conseguenza, gli SDK nativi non vengono utilizzati.

 

### Altre architetture

Oltre alle due architetture principali basate su REST API, soluzioni client server-to-server e Direct per dispositivi avanzati, esistono altre architetture.  Principale tra questi è l&#39;architettura SDK, che utilizza un componente client denominato Access Enabler che l&#39;autenticazione Primetime fornisce ai programmatori.  L’app utilizza le API di Access Enabler per gestire l’avvio, l’autenticazione, l’autorizzazione e l’logout.  Tutte le comunicazioni tra l&#39;app del programmatore e i server di autenticazione Primetime si verificano tramite Access Enabler.  È disponibile una versione diversa di Access Enabler per le seguenti piattaforme: JavaScript, iOS, tvOS, Android e FireTV.

Anche se è possibile utilizzare l’API REST direttamente sulle piattaforme client che supportano SDK nativi al di fuori di una soluzione Server-to-Server, questo approccio non è consigliato.

 

## Pro e cons dell’API REST {#ProsAndCons}

L’API REST di autenticazione Adobe Primetime è stata creata per fornire una soluzione TVE (TV Everywhere) per i dispositivi che non dispongono di funzionalità di navigazione web o di archiviazione permanente. L’API REST fornisce il supporto per tutti i flussi di autenticazione e autorizzazione, ma perché manca un componente SDK nativo. Gli SDK forniti e mantenuti da Adobe Primetime Authentication forniscono funzionalità predefinite che implementano regole aziendali che in caso di REST API devono essere implementate e gestite dai programmatori. Nella tabella Responsabilità programmatore riportata di seguito descriviamo i limiti dell’API REST corrente che devono essere risolti dai programmatori.

 

### Server-to-server e Pro e Cons basati su client

Un&#39;architettura server-to-server consente di consolidare la maggior parte della logica relativa all&#39;autenticazione e all&#39;autorizzazione in un&#39;unica unità logica o implementazione.  Questo approccio ha pro e contro.  I pro includono:

* Implementazione singola per logica di business di autenticazione e autorizzazione.
* Evita di implementare tale logica su ogni piattaforma supportata utilizzando gli strumenti nativi delle piattaforme.
* La possibilità di aggiornare le funzionalità senza dover aggiornare i client con tutti i relativi requisiti associati (ad esempio gli aggiornamenti dell’app store).
* **Più semplice** estendere e personalizzare le funzionalità authN e authZ (ad esempio aggiungere D2C).
* Gestione diretta del traffico associato per un maggiore controllo, qualità e monitoraggio.

 

Anche in questo caso, gli svantaggi sono elencati nelle responsabilità del programmatore, ma includono quanto segue:

* L’SSO deve essere implementato per ogni client per piattaforme senza SSO piattaforma.
* Se necessario, i programmatori devono implementare una logica specifica per MVPD.
* Tutte le piattaforme che utilizzano l’API REST condividono una singola configurazione che regola proprietà come TTL di autenticazione.

 

### Dispositivi collegati

Per la maggior parte dei dispositivi connessi, l’API REST deve essere utilizzata in un modo o nell’altro, poiché un SDK non è disponibile. Il dispositivo connesso utilizzerà direttamente l’API REST oppure si integrerà con una soluzione Server-to-Server che utilizza l’API REST.

## Responsabilità del programmatore {#programmer-responsibilities}

Le seguenti informazioni si applicano sia alle applicazioni server-to-server che a quelle collegate ai dispositivi.

| **Funzionalità** | **Responsabile della gestione della funzionalità** | **Descrizione delle limitazioni dell’API Clientless corrente e delle differenze rispetto agli SDK nativi** |
| --- | --- | --- |
| Impostazioni di configurazione applicate per piattaforma | Adobe | Uno **limitazione importante** sull’utilizzo dell’API REST in tutte le piattaforme (inclusi i dispositivi mobili come iOS e Android) è che le impostazioni di configurazione corrispondenti all’API REST nel nostro strumento di configurazione TVE Dashboard vengono applicate su tutti i dispositivi (anche se è presente un dispositivo iOS che esegue un’applicazione nativa implementata sopra la nostra API REST). Questa limitazione **può rompersi** i TTL concordati e le impostazioni della piattaforma concordate con gli MVPD - se questi differiscono per ciascuna piattaforma. [1](#1) |
| Single Sign-On | Programmatori | Utilizzando l’API REST, l’SSO è disponibile solo sulle piattaforme che supportano l’SSO della piattaforma (ad esempio Apple, Roku, Amazon), mentre l’SSO non può essere garantito per altre piattaforme quando si utilizza l’API REST. Gli SDK memorizzano i dati nella cache in modo cross-site/app. Ciò significa che l&#39;utente effettua l&#39;accesso una volta su un sito/app e ha già effettuato l&#39;accesso sui siti partecipanti, senza che sia necessaria alcuna interazione con l&#39;utente. [2](#2) |
| Disconnessione singola | Programmatori | In uno scenario SSO SDK nativo, la disconnessione da un&#39;applicazione partecipante disconnette l&#39;utente da qualsiasi luogo. SLO non è supportato nell’API REST corrente. La disconnessione da un’applicazione disconterà l’utente solo per quella particolare applicazione. |
| Memorizzazione in cache | Programmatori | Le implementazioni REST API dovranno implementare il proprio meccanismo di caching per gli elementi di dati concordati per le aziende. Gli SDK memorizzano automaticamente nella cache vari elementi di dati, tenendo conto di varie regole aziendali. Ad esempio, i metadati utente vengono memorizzati nella cache con lo stesso TTL del token di autenticazione, mentre alcuni elementi possono essere esclusi programmaticamente dalla memorizzazione in cache (preflight). |
| Meccanismo dettagliato di segnalazione degli errori | Programmatori | L’API REST si basa principalmente sui codici di errore HTTP per segnalare gli errori dell’applicazione, mentre gli SDK dispongono di un meccanismo di segnalazione degli errori dettagliato che consente agli sviluppatori dell’applicazione di comprendere meglio cosa sta succedendo. |
| Ripristino degli errori dell&#39;applicazione (esecuzione di un nuovo tentativo in caso di errore, rilevamento del loop, ecc.) | Programmatori | Le implementazioni API REST devono creare i propri sistemi di ripristino delle applicazioni, mentre le implementazioni oltre agli SDK beneficiano del sistema di recupero degli errori degli SDK: ripristino da errori di rete transitori, riprovando alcune chiamate di rete con logica esistente per evitare i &quot;loop&quot;. |
| Autenticazione per richiedente | Programmatori | Alcuni MVPD richiedono l’autenticazione per ogni sito/app, per motivi aziendali o a causa di problemi tecnici. Gli SDK lo applicano automaticamente in base alla configurazione del dashboard TVE. I implementatori API REST devono implementarlo autonomamente, al fine di non violare gli accordi commerciali, o per essere in grado di completare l’autorizzazione per quegli MVPD che rientrano nei loro dati di autenticazione per applicazione. |
| Autenticazione passiva | Programmatori | Alcuni MVPD supportano l’autenticazione &quot;passiva&quot;, in cui l’utente non è tenuto a immettere le credenziali, e viene effettuato automaticamente un tentativo di autenticazione dell’utente. Questo è particolarmente utile per gli MVPD che hanno anche &quot;Authentication per requestor&quot; come requisito. In questo caso, l’UX abilitato dagli SDK è invisibile, in cui l’utente esegue l’autenticazione solo una volta in un’applicazione e l’SDK esegue l’autenticazione &quot;passiva&quot; per altre applicazioni nell’ecosistema. L&#39;utente non vede le chiamate passive aggiuntive, sarà semplicemente già autenticato, mentre l&#39;MVPD raggiunge l&#39;obiettivo di avere sessioni di autenticazione separate per ogni applicazione. |
| Rilevamento dei dispositivi uniforme e implicito | Programmatori | Gli SDK rilevano automaticamente il tipo di dispositivo e inviano tali informazioni in modo standard. Le implementazioni delle API REST sono soggette all’invio di informazioni diverse, a seconda dell’implementatore, modificando le regole e le statistiche aziendali in modo approssimativo e corrompendo in tal modo le statistiche sui diversi siti. **I programmatori devono assicurarsi che ci abbiano inviato informazioni corrette sui dispositivi** su ciascuna delle loro app. Per le implementazioni server-to-server, l’api REST non identifica correttamente l’indirizzo IP dell’utente finale, a meno che non vengano eseguiti ulteriori passaggi. L&#39;indirizzo IP è importante in alcuni casi d&#39;uso come la prevenzione delle frodi o l&#39;HBA. |
| TempPass a prova di manomissione | Programmatori | L&#39;applicazione di TempPass è basata su un ID dispositivo stabile. Gli SDK utilizzano tecniche di informazione/impronta digitale hardware per identificare il dispositivo e questo meccanismo non è pubblico, quindi più sicuro e privo di conflitti. Per le implementazioni API REST, i programmatori devono implementare i propri algoritmi per l’identificazione/impronte digitali dei dispositivi. |
| Associazione dispositivo | Programmatori | I token generati su un dispositivo con un’applicazione tramite SDK non sono portatili, il che rende difficile per un utente malintenzionato condividere i suoi token e fornire l’accesso ad altri utenti. Si basa sullo stesso meccanismo ID dispositivo del &quot;TempPass a prova di manomissione&quot;. Per l’API REST, i token rimangono nel cloud, il che significa che due dispositivi con lo stesso deviceID che effettuano le stesse chiamate riceveranno le stesse risposte/accessi. I programmatori devono assicurarsi di disporre di un meccanismo solido, sicuro e privo di conflitti per generare/allocare gli ID dispositivo. |
| Prevedibile e certificato insieme di funzioni | Programmatori | Il set di funzioni esistente in ogni SDK è coerente, prevedibile e certificato e testato completamente. Alcuni requisiti aziendali vengono applicati tramite gli SDK, il che rende rischioso per il programmatore violare i contratti utilizzando l’API REST. Anche se l’API REST potrebbe essere più flessibile, l’Adobe garantisce che le implementazioni SDK applichino le decisioni aziendali e le impostazioni dalla dashboard TVE. Nel caso di Clientless, ogni programmatore implementa il proprio sottoinsieme delle regole aziendali che suite le proprie applicazioni in un dato momento. |


1. Come parte della nostra nuova iniziativa One API, prevediamo di correggere questa limitazione e di poter applicare regole per piattaforma in base all’identificazione del dispositivo.

2. Adobe continua a lavorare con tutte le principali piattaforme per implementare Platform SSO che può essere utilizzato con la nostra API REST. La nostra iniziativa One API offrirà il supporto SSO tra le app implementate utilizzando SDK nativi e le app implementate tramite API REST.

## Requisiti minimi del dispositivo {#min_reqs}

Per utilizzare l’API REST di autenticazione di Primetime, i dispositivi devono soddisfare o superare i requisiti tecnici minimi elencati nella sezione REST API della [Documento sui requisiti di Primetime Authentication Platform / Device / Tools](#general_clientless_reqs).


