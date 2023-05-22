---
title: Informazioni sull’autenticazione di Adobe Primetime e TV Everywhere
description: Informazioni sull’autenticazione di Adobe Primetime e TV Everywhere
exl-id: 5edeaccb-f9fa-4395-83b4-706c518d5a03
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '6288'
ht-degree: 0%

---

# Informazioni sull’autenticazione di Adobe Primetime e TV Everywhere {#about-auth-tve}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Informazioni sulla TV Ovunque {#about-tve}

I telespettatori di oggi possono andare online in qualsiasi momento o luogo, e si aspettano che la loro capacità di accedere ai contenuti della Pay TV sia proprio lì con loro. Inoltre, il pubblico sta visualizzando i contenuti utilizzando una gamma sempre più ampia di dispositivi compatibili con Internet, tra cui:

* Notebook
* Compresse
* Smartphone
* Siti Web
* App federate
* Console di gioco
* Set-top box
* Smart TV

TV Everywhere è il movimento di settore che supporta la capacità degli abbonati alla Pay TV di accedere agli stessi contenuti che stanno già pagando, su più dispositivi, sia dentro che fuori dalle loro case. Mentre la maggior parte della visione televisiva avviene ancora su televisori convenzionali e lineari, la crescita del consumo è nei contenuti spostati nel tempo, nei video online e negli schermi alternativi. Di conseguenza, il mercato della distribuzione di video oggi è in uno stato di perturbazione, e TV Everywhere è emersa come la soluzione che allinea gli interessi dei programmatori, dei fornitori di televisione a pagamento e degli abbonati alla Pay TV.


L&#39;obiettivo tecnico di TV Everywhere è quello di consentire ai clienti di PayTV di accedere ai contenuti a cui sono già abbonati su tutti i loro dispositivi e piattaforme.


Gli obiettivi aziendali di TV Everywhere sono:

* **Mantenere le relazioni con i clienti esistenti e abilitarne di nuove**
* Consentire ai programmatori e ai proprietari dei contenuti di raggiungere il pubblico più ampio e di acquisire più valore dai contenuti premium
* Estendere i brand tramite interazione diretta online con i visualizzatori

## Le sfide di TV Everywhere {#tve-challenges}

Oltre alle opportunità offerte da TV Everywhere, ci sono delle sfide da affrontare. Il nocciolo di queste è l&#39;adesione. Prima che un visualizzatore acceda al contenuto dell’abbonamento, è necessario che qualcuno determini se ha diritto a tale accesso.

L&#39;utente dispone di un abbonamento con un provider di servizi di televisione a pagamento? In caso affermativo, tale abbonamento include il contenuto richiesto? L&#39;adesione è particolarmente difficile da determinare direttamente per i programmatori e i proprietari dei contenuti, perché sono gli operatori di televisione a pagamento che dispongono dei dati di identificazione per i loro clienti e dei loro privilegi di accesso.


Oltre all’adesione, esistono una serie di problemi tecnici e di integrazione correlati, tra cui:

* Sviluppo e implementazione di una strategia completa multi-dispositivo
* Coordinamento delle molteplici relazioni tra programmatori e fornitori di servizi di televisione a pagamento
* Prevenzione dell&#39;accesso fraudolento o dell&#39;abuso dei termini di servizio
* Fornire un’esperienza di autenticazione coerente e priva di frustrazioni per gli utenti tra siti web e app
* Mantenere un rapido time-to-market per tenere il passo con le offerte affiliate
* Gestione dei costi associati a più integrazioni

Queste sfide rendono l&#39;esecuzione e la manutenzione di complesse integrazioni dirette tra i programmatori e i sistemi di autenticazione di più provider di Pay TV altamente dispendiosi in termini di risorse, richiedendo tempo e complessità tecnica.


La soluzione? **Adobe ® Autenticazione Primetime**.

## Introduzione all’autenticazione di Adobe Primetime {#authentication-intro}

Con l’autenticazione Adobe Primetime, i programmatori e i provider di servizi di televisione a pagamento devono eseguire solo una semplice integrazione, utilizzando le API di autenticazione Adobe Primetime, per accedere all’intero ecosistema, tra cui:

* Programmatori come Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks e Hulu

* Tutti i principali fornitori di Pay TV negli Stati Uniti, che comprendono oltre il 90% di tutte le famiglie di Pay TV negli Stati Uniti

Inoltre, l’autenticazione Adobe Primetime fornisce il framework che rende l’autenticazione e l’autorizzazione degli utenti semplici e sicure.

![](assets/programmers-connect-authn.png)

*Figura 1: Solo alcuni dei programmatori e provider di servizi di televisione a pagamento che si connettono tramite autenticazione Adobe Primetime...*

Adobe Pass gestisce in modo sicuro le transazioni di adesione tra programmatori e fornitori di servizi di televisione a pagamento, facilitando l’accesso degli utenti ai contenuti in abbonamento. Oppure, in altre parole...

**L’autenticazione Adobe Primetime consente ai clienti giusti di accedere in modo semplice e rapido ai contenuti corretti.**

**Per chi è l’autenticazione Adobe Primetime?**

* **Programmatori** che desiderano integrarsi facilmente con i provider di servizi di televisione a pagamento (noti anche come &quot;MVPDs&quot; o &quot;Multichannel Video Programming Distributors&quot;), raggiungendo il pubblico più ampio, per ottenere ricavi ottimali. Utilizzando l’autenticazione Adobe Primetime, i programmatori possono autenticare i visualizzatori tra tutti i principali provider, indipendentemente dalla piattaforma client.

* **Provider di servizi di televisione a pagamento/MVPD** che cercano una connettività indolore con più programmatori e una maggiore soddisfazione dei clienti facilitando l’accesso online ai contenuti in abbonamento.

* **Clienti di Pay TV** che desiderano poter accedere facilmente ai contenuti a cui si sono già iscritti, ovunque si trovino, senza costi aggiuntivi. Il Single Sign-On fornisce l&#39;autenticazione protetta del visualizzatore in tutto il Web o nelle app mobili, senza richiedere download client o accessi ripetuti, nonché una buona esperienza utente.

Per **Programmatori**, l’autenticazione Adobe Primetime fornisce:

* Integrazione semplice e connettività immediata con i principali provider di Pay TV, senza il dolore di molteplici integrazioni dirette
* Ottimizzazione sia dei ricavi derivanti dall’abbonamento (licenze) che da quelli pubblicitari grazie al supporto di un pubblico il più ampio possibile di contenuti
* Autenticazione sicura, con accesso ai contenuti premium concesso solo a utenti/dispositivi autorizzati
* Un framework aperto e flessibile che è indipendente dal lettore e dalla piattaforma DRM; la riproduzione può verificarsi su un’ampia gamma di piattaforme, tra cui iOS, Android, Windows 8, console di gioco, set-top box e altro ancora.
* Compatibilità con qualsiasi tecnologia DRM, ad esempio Flash Access di Adobe ® o Play Ready®.
* Supporto per l&#39;autenticazione e l&#39;autorizzazione Single Sign-On (SSO), in modo che i sottoscrittori non debbano effettuare di nuovo l&#39;accesso dopo la prima autenticazione sul proprio sistema.


Per **Provider di servizi di televisione a pagamento/MVPD**, l’autenticazione Adobe Primetime fornisce:

* Facile integrazione con i proprietari dei contenuti, grazie alla possibilità di connessione immediata con più programmatori tramite un&#39;unica integrazione
* È stato migliorato il coinvolgimento dei clienti grazie al supporto di un’esperienza fluida e di marca nella visualizzazione dei contenuti su più piattaforme e dispositivi
* Autenticazione sicura che garantisce che solo gli utenti/dispositivi autorizzati possano accedere ai contenuti premium e (facoltativamente) limita il numero di dispositivi e flussi simultanei che possono connettersi per ogni account domestico.


Per **Clienti di Pay TV**, l’autenticazione Adobe Primetime fornisce:

* **TV Ovunque!**

Il resto di questo documento fornisce un’introduzione tecnica all’autenticazione Adobe Primetime.  Mentre molte delle seguenti si concentrano sull’integrazione dei programmatori, esistono informazioni sia generali che specifiche che si applicano anche ai fornitori di servizi di televisione a pagamento. Questo documento evidenzia anche la sicurezza e l&#39;integrità del funzionamento dell&#39;autenticazione Adobe Primetime come soluzione per TV Everywhere. Per ulteriori dettagli oltre a questo documento, contatta il rappresentante del tuo Adobe o compila il modulo di richiesta di informazioni [qui](https://www.adobe.com/).

## Elementi di base dell’architettura {#arch-building-blocks}

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/import-pc7mz3dfnv/check.gif) Di seguito vengono descritte le transazioni di autenticazione e autorizzazione centralizzate. Per autenticazione si intende il processo di conferma con un provider di Pay TV che un determinato utente è un cliente noto. L&#39;autorizzazione è il processo in cui un provider di Pay TV conferma che un utente autenticato dispone di un abbonamento valido a una determinata risorsa.
L’autenticazione Adobe Primetime è costituita dai seguenti componenti di base:

* Componente client (uno dei seguenti):

   * Access Enabler: libreria specifica per la piattaforma che fornisce API ed esempi di codice di facile utilizzo per l’implementazione dei flussi di adesione
   * API senza client: servizi web RESTful; fornisce endpoint di flusso di adesione per piattaforme senza funzionalità di rendering delle pagine web (come console di giochi, set-top box, ecc.)

* Server back-end ospitati da Adobi
* Il Media Token Verifier
* Un mezzo di scambio centrale sicuro (token)

A livello di base, l’autenticazione Adobe Primetime è costituita da tre componenti (l’Access Enabler, i server back-end ospitati dall’Adobe e il Media Token Verifier) e da un elemento centrale di scambio (token).

### Componenti client {#client-components}

* Access Enabler
* API senza client

#### Access Enabler {#access-enabler}

Sulle piattaforme completamente supportate (tra cui Web, iOS, Android, Windows 8), i programmatori interagiscono con l’autenticazione di Adobe Primetime tramite il componente client di Access Enabler. Questo componente facilita tutte le interazioni di autenticazione e autorizzazione con il cliente.  Access Enabler viene eseguito localmente sul sistema. Quando un utente accede a un sito o a un’applicazione Programmatore e richiede contenuto, il componente Access Enabler gestito/ospitato dall’Adobe viene caricato in background.

L’Access Enabler gestisce i flussi di lavoro effettivi per l’adesione, mentre il Programmatore mantiene la responsabilità per la pagina web di livello superiore o l’applicazione del lettore che implementa l’interfaccia utente e interagisce con l’Access Enabler. Queste interazioni avvengono tramite un sistema asincrono di funzioni e callback, definiti dall’API di Access Enabler.

Questi sono i flussi di adesione di base, facilmente implementabili utilizzando l’API di Access Enabler:

* Impostazione dell&#39;identità del richiedente (programmatore)
* Verifica/ottenimento dell’autenticazione dell’utente per un determinato operatore di Pay TV (il &quot;provider di identità&quot;)
* Verifica/ottenimento dell&#39;autorizzazione utente per una risorsa specifica
* Disconnessione dell&#39;utente

Access Enabler fornisce inoltre i seguenti servizi:

* Convalida le query del Programmatore, incluso lo stato di registrazione di client specifici, i loro domini e le loro risorse/canali.
* Fornisce i dati che creano l’elenco degli operatori di televisione a pagamento da cui l’utente seleziona il proprio fornitore. Questo elenco viene inoltre convalidato e definito in modo appropriato per il programmatore da cui ha origine la richiesta.
* Avvia flussi di lavoro di autenticazione e autorizzazione specifici per gli operatori di Pay TV.
* Memorizza nella cache le risposte di autorizzazione riuscite per risorsa/canale del programmatore per ridurre al minimo il traffico di richieste non necessario.
* Può essere configurato per flussi di lavoro predefiniti specifici per ciascun operatore di Pay TV, ad esempio per la registrazione esplicita del dispositivo.

A seconda del sito web o dell’applicazione lettore, l’Access Enabler può assumere le seguenti forme:

* Un file SWF che il runtime di Flash Player può eseguire
* Un file JS eseguito direttamente dal browser
* Un Access Enabler nativo per le piattaforme supportate (tra cui iOS, Android e Windows 8)

#### API senza client {#clientless-api}

L’approccio API senza client è per i &quot;dispositivi avanzati&quot; (console di giochi, set-top box e Smart TV) che non supportano i browser web (necessari per l’autenticazione con MVPD).  Nell’approccio senza client, le app per dispositivi avanzati comunicano direttamente con l’autenticazione di Adobe Primetime tramite le API dei servizi web RESTful per tutto, eccetto l’autenticazione, che viene eseguita su un’app nella seconda schermata (browser). In altre parole, la libreria lato client di Access Enabler non viene utilizzata. Al contrario, gli sviluppatori di app per dispositivi avanzati utilizzano direttamente le API dei servizi web di autenticazione di Adobe Primetime per implementare i flussi di adesione.

### Server back-end ospitati da Adobi {#adobe-backend-servers}

I server back-end di autenticazione Adobe Primetime, ospitati da Adobe:

* Fornire i flussi di lavoro di autenticazione e autorizzazione ai provider di servizi di televisione a pagamento che richiedono la comunicazione server-to-server tra l’autenticazione di Adobe Primetime e l’operatore.
* Gestisci la configurazione per i siti e le applicazioni del programmatore.
* Ospita i file dei componenti scaricabili di Access Enabler.
* Fornisci gli endpoint del servizio web RESTful per l’integrazione API senza client.
* Generare (e in alcuni casi archiviare) token di autenticazione e autorizzazione.

### Token e Media Token Verifier {#tokens-media-token-verifier}

La soluzione Adobe Primetime per l’autenticazione è incentrata sulla generazione di parti specifiche di dati ottenuti al completamento dei flussi di lavoro di autenticazione/autorizzazione. Questi dati sono denominati token. Hanno una durata limitata e sono archiviati in modo sicuro, sia in posizioni dipendenti dalla piattaforma sul client che su server di Adobe, nel caso della soluzione API senza client. Alla scadenza, i token devono essere ririlasciati riavviando i flussi di lavoro di autenticazione e/o autorizzazione.

Esistono tre tipi di token che l’autenticazione Adobe Primetime genera durante i flussi di lavoro di autenticazione/autorizzazione. Due sono &quot;di lunga durata&quot; e forniscono continuità nell’esperienza di visualizzazione dell’utente. Il terzo, un token di breve durata, fornisce supporto per le best practice del settore per mitigare le frodi (dove le frodi includono exploit come ad esempio la copia di flussi). I valori TTL (time-to-live) sono impostati in base agli accordi tra i programmatori e i provider di servizi di televisione a pagamento, che concordano su un valore più adatto a tutte le persone coinvolte.

#### Token di autenticazione (di lunga durata) {#long-lived-auth-token}

L’autenticazione viene eseguita correttamente quando un cliente utilizza l’autenticazione Adobe Primetime per accedere al proprio account Pay TV. L’autenticazione Adobe Primetime genera quindi un token di autenticazione di lunga durata (AuthN) associato al dispositivo richiedente e (a seconda del provider di Pay TV) un identificatore univoco globale (&quot;GUID&quot;) che identifica l’utente in modo anonimo.

* L’autenticazione Adobe Primetime memorizza il token AuthN in modo sicuro in un percorso in cui è disponibile per tutte le applicazioni che utilizzano l’autenticazione Adobe Primetime. Per le integrazioni con Access Enabler, i token vengono memorizzati in modo sicuro sul lato client.  L’autenticazione Adobe Primetime utilizza il token AuthN per eseguire query di autorizzazione successive per conto dell’utente.
* In un dato momento viene archiviato un solo token AuthN. Ogni volta che viene rilasciato un nuovo token AuthN e ne esiste già uno vecchio, il nuovo token sovrascrive il valore memorizzato esistente.

#### Token di autorizzazione (di lunga durata) {#long-lived-authriz-token}

In caso di esito positivo dell’autorizzazione, l’autenticazione Adobe Primetime crea un token di autorizzazione di lunga durata (&quot;AuthZ&quot;). Questo token non è portatile, in quanto è associato al dispositivo richiedente e a una risorsa protetta specifica (ad esempio, un canale, una serie o un episodio).

* L’autenticazione di Adobe Primetime memorizza il token AuthZ in modo sicuro, insieme ad altri token di autorizzazione per altre risorse.  Anche in questo caso, come per i token AuthN, nelle piattaforme che utilizzano l’Access Enabler il token viene memorizzato localmente sul client; nelle piattaforme che utilizzano l’API senza client, i token vengono memorizzati sui server di autenticazione di Adobe Primetime.
* Il valore TTL (time-to-live) del token AuthZ di lunga durata viene in genere definito nell’intervallo tra giorni e settimane, a seconda dell’accordo specifico tra il provider di Pay TV e il programmatore.
* In un dato momento viene memorizzato un solo token AuthZ per risorsa. Possono essere memorizzati più token di autorizzazione, purché associati a risorse diverse. Ogni volta che viene rilasciato un nuovo token di autorizzazione e ne esiste già uno per la stessa risorsa, il nuovo token sovrascrive il valore memorizzato nella cache esistente.
* L’autenticazione di Adobe Primetime utilizza il token AuthZ di lunga durata per creare i token multimediali di breve durata utilizzati per l’accesso effettivo alla visualizzazione.

#### Token di file multimediali a breve durata {#short-lived-media-token}

Una volta generato il token AuthZ, Adobe Primetime lo utilizza per generare un token multimediale monouso di breve durata firmato da Adobe e crittografato per evitare manomissioni durante lo scambio:

* Il TTL del token di breve durata (impostazione predefinita: 5 minuti) è impostato per consentire problemi di sincronizzazione dell’orologio tra il server che genera il token e il server che lo convalida.
* Il token di breve durata viene esposto al sito di incorporamento prima di fornire l’accesso alla risorsa protetta, pertanto il programmatore deve convalidarlo, utilizzando Media Token Verifier per le integrazioni di Access Enabler, o Token Verifier Service nel caso di integrazioni API senza client.

#### Media Token Verifier {#media-token-verifier}

I programmatori sono responsabili dell’integrazione della Media Token Verifier Library nel loro application server esistente, in modo che il verificatore possa eseguire le convalide dell’utente finale prima dell’effettivo avvio di un flusso video. La libreria Media Token Verifier definisce:

* API di verifica dei token che recupera informazioni dal token, ad esempio se è valido, l’ora in cui è stato emesso il token e altri dati rilevanti
* Chiave pubblica di Adobe utilizzata per verificare che il token provenga effettivamente da Adobe
* Un’implementazione di riferimento che mostra come utilizzare l’API del verificatore e come utilizzare la chiave pubblica di Adobe contenuta nella libreria per verificarne l’origine

![](assets/high-level-architecture-nflows.png)

*Figura 2: Architettura di alto livello dell’ecosistema di autenticazione Adobe Primetime in un’integrazione di Access Enabler*

## Integrare con l’autenticazione di Adobe Primetime {#integrate-auth}

Che tu sia un provider di Pay TV o un programmatore, il processo di integrazione con l’autenticazione di Adobe Primetime richiede una parte della tua partecipazione attiva. Ciascuno di questi processi è descritto di seguito.

### Processo provider di servizi di televisione a pagamento

La responsabilità principale del provider di Pay TV per l&#39;autenticazione di Adobe Primetime consiste nel verificare che l&#39;utente richiedente sia effettivamente un abbonato noto autorizzato ad accedere al contenuto del programmatore. Ad alto livello, il processo di autenticazione di Adobe Primetime per l’integrazione con un nuovo provider di Pay TV richiede i seguenti passaggi:

1. Il provider firma l’accordo di non divulgazione (NDA) per l’autenticazione di Adobe Primetime.
1. Il provider fornisce all&#39;Adobe le specifiche per i propri sistemi di autenticazione e autorizzazione. Per un’integrazione più semplice, si consiglia agli operatori di Pay TV di disporre di un provider di identità (IdP) basato su SAML per l’autenticazione e la capacità di comunicare tramite il protocollo di accesso SOAP per l’autorizzazione.
1. Il provider stabilisce la connettività tra i propri server e i server di autenticazione di Adobe Primetime. Ciò include la fornitura degli endpoint e l’elenco degli IP.
1. Versione di pre-qualifica e QE.
1. Release di produzione e QE.

Anche se l’autenticazione Adobe Primetime può sostituire le integrazioni esistenti per i programmatori, in genere questa operazione non è richiesta per i provider di servizi di televisione a pagamento. Adobe collabora con il team tecnico del provider per configurare l’autenticazione di Adobe Primetime in modo da soddisfare le esigenze di eventuali integrazioni esistenti. L’integrazione è gratuita per i provider di servizi di televisione a pagamento, supponendo un’integrazione &quot;standard&quot; e requisiti minimi di supporto (documentazione e supporto e-mail di base). Se un fornitore richiede un supporto significativo o una tempistica aumentata, potrebbe essere addebitata una tariffa di supporto o il fornitore potrebbe voler lavorare con una terza parte a conoscenza della nostra soluzione, come Synacor.


L’autenticazione Adobe Primetime supporta anche la gestione efficiente della logica di business del provider di servizi di televisione a pagamento, come segue:

* Per la logica di business indipendente e che può essere applicata dall’operatore quando viene ricevuta una richiesta di autorizzazione, Adobe fornisce i dati necessari necessari per supportare l’applicazione della logica di business quando l’operatore riceve una richiesta di autorizzazione. Questi dati possono includere, ma non essere limitati a, l’ID dispositivo univoco per l’utente che effettua la richiesta e l’indirizzo IP del dispositivo.
* Per la logica di business che richiede l’intervento dell’utente e/o la gestione specifica da parte della soluzione di Adobe, Adobe può mantenere alcune proprietà personalizzate per ogni provider di Pay TV. Queste configurazioni/policy specifiche dell’operatore includono l’abilitazione di flussi di lavoro predefiniti che possono essere avviati in punti specifici del flusso di lavoro di livello superiore. Per informazioni dettagliate sul supporto delle proprietà personalizzate, contatta il rappresentante del tuo Adobe.

Adobe offre anche servizi che limitano le frodi. Per ulteriori informazioni, contatta il rappresentante di Adobe.

### Il processo del programmatore {#programmer-process}

Per integrare correttamente l’autenticazione Adobe Primetime, i programmatori devono configurare l’applicazione o la pagina web del lettore multimediale per interagire con l’autenticazione Adobe Primetime nella gestione dei processi di adesione di base: autenticazione, autorizzazione e disconnessione.


Prima di iniziare un’integrazione con l’autenticazione Adobe Primetime, i programmatori devono disporre di:

* Piattaforma video online esistente, incluso un lettore multimediale, come parte di un sito web o come applicazione autonoma
* Un sistema di gestione dei contenuti
* Un meccanismo di distribuzione, che può includere o meno una rete per la distribuzione di contenuti (CDN) di terze parti

I programmatori dovrebbero aspettarsi di eseguire alcune attività di integrazione nell&#39;ambito della fornitura di servizi TV Everywhere con l&#39;autenticazione Adobe Primetime. Queste attività includono:

* Integrazione della libreria Access Enabler di Adobe Primetime Authentication nella pagina web o nel lettore multimediale o implementazione dell’integrazione utilizzando l’approccio Clientless per &quot;dispositivi avanzati&quot; che non supportano il web
* Lavoro lato server per integrare il componente Adobe Primetime Authentication Token Verifier nel flusso di lavoro di streaming video
* Creazione di un’interfaccia utente per il flusso di lavoro di accesso nel sito web o nell’app (alcuni elementi, come il processo di accesso effettivo, sono forniti dall’operatore di Pay TV e altri sono facoltativamente disponibili come parte dell’autenticazione di Adobe Primetime)

Questo documento fornisce una panoramica della procedura del programmatore e un Adobe fornisce ulteriori indicazioni sull’avvio formale dell’integrazione.

#### Impostazione richiedente (programmatore) {#requester-prog-setup}

##### Registrazione con Adobe {#registering}

Come primo passo, i programmatori devono registrarsi presso Adobe o un partner autorizzato da Adobe e specificare i domini che desiderano utilizzare con l’autenticazione Adobe Primetime. I programmatori ricevono quindi un ID richiedente univoco, fornito all’autenticazione di Adobe Primetime per ogni sessione in cui il programmatore interagisce con Access Enabler.

##### Impostazione Dell&#39;Integrazione Initial Access Enabler {#access-enabler-int-setup}

Prima di qualsiasi cliente che richieda l’accesso al contenuto, i programmatori devono integrare il componente client di autenticazione di Adobe Primetime, Access Enabler, nell’app o nella pagina web del lettore multimediale esistente. Per eseguire questa operazione sono disponibili varie opzioni:

* Puoi incorporare la versione del Flash, AccessEnabler.swf, in un lettore video basato su Flash in una pagina web o direttamente in HTML. Puoi comunicare con il SWF in ActionScript o JavaScript. L’API di base è ActionScript, ma è disponibile una libreria wrapper JavaScript completa.
* Per i dispositivi non di Flash, è possibile:
   * Utilizza la versione HTML5/JavaScript di AccessEnabler.js e comunica con essa tramite l’API JavaScript, oppure
   * Utilizza una libreria nativa di Access Enabler, ad esempio per iOS, Android o Windows 8

##### Configurazione per l’integrazione API iniziale senza client {#clientless-api-int-setup}

Prima di qualsiasi cliente che richieda l’accesso al contenuto, i programmatori devono implementare le chiamate ai servizi web RESTful utilizzando l’API Clientless nell’app del lettore multimediale, nonché configurare un’applicazione &quot;second-screen&quot; per gestire l’accesso dell’utente al proprio provider Pay TV via web.

#### Gestione dell’autenticazione e dell’autorizzazione {#auth-authr-handling}

Quando un cliente richiede una risorsa protetta a un programmatore per la prima volta, il programmatore presenta al cliente un elenco di fornitori di televisione a pagamento tra cui scegliere. Quando il provider è selezionato, l&#39;utente viene reindirizzato a tale operatore per l&#39;autenticazione utente iniziale. Una volta completata l&#39;autenticazione, Adobe Primetime comunica con il provider di Pay TV selezionato per autorizzare l&#39;accesso alla risorsa specificata. Di seguito sono riportati i dettagli di questi processi.

![](assets/providr-selection-ui.png)


*Figura 3: Esempio di interfaccia utente per la selezione dei fornitori*

>[!NOTE]
>
>* L’autenticazione si verifica come scambio SAML tra l’autenticazione di Adobe Primetime come provider di servizi (o &quot;SP&quot;) e un provider di Pay TV come provider di identità (o &quot;IdP&quot;).
>* L’autorizzazione utilizza uno scambio di servizi web back-channel (server-to-server) tra l’autenticazione di Adobe Primetime (SP) e un provider di Pay TV (IdP).



##### Comunicazione dei programmatori tramite Access Enabler

Il canale di comunicazione bidirezionale tra Access Enabler e la pagina web o l’app del programmatore segue uno schema completamente asincrono. Il programmatore invia messaggi all&#39;Access Enabler tramite i metodi esposti dall&#39;API Access Enabler. Access Enabler risponde tramite callback registrati con la libreria Access Enabler.

* Se nel sistema locale non viene trovato alcun token di autenticazione, qualsiasi richiesta di autorizzazione richiede automaticamente prima l’autenticazione. Quando l’autenticazione ha esito positivo, il token del cliente viene memorizzato localmente, in modo che non sia necessario effettuare nuovamente l’accesso per un determinato periodo di tempo. Se l&#39;autenticazione è stata eseguita correttamente tramite la soluzione di autenticazione di Adobe Primetime in qualsiasi altro contesto (ad esempio, tramite il sito Web del provider di Pay TV o un altro programmatore), Access Enabler ha accesso al token locale e non richiede l&#39;esecuzione di un&#39;autenticazione aggiuntiva.
* Quando un cliente richiede una risorsa specifica, il programmatore richiede l’autorizzazione al provider di Pay TV tramite Access Enabler. Dopo aver verificato (o avviato) l’autenticazione, Access Enabler contatta il provider di Pay TV (tramite l’autenticazione di Adobe Primetime) per determinare se il cliente ha il diritto di visualizzare la risorsa. L’autenticazione Adobe Primetime gestisce la comunicazione con il provider di Pay TV per ottenere l’autorizzazione. Il programmatore deve solo inviare la richiesta all’Access Enabler e gestire la risposta (esito positivo o negativo dell’autorizzazione). Se l&#39;autorizzazione ha esito positivo, nel sistema client viene memorizzato un token di autorizzazione e il callback riceve un token multimediale di breve durata.

##### Comunicazione dei programmatori tramite l’API Clientless {#progr-comm-clientless-api}

La comunicazione tra l’app del programmatore e l’autenticazione Adobe Primetime avviene tramite i servizi web RESTful.  Sono disponibili protocolli di sicurezza per tutte le chiamate API agli endpoint di autenticazione di Adobe Primetime.  I requisiti di sicurezza sono descritti nella documentazione dell’API senza client.

##### Flusso di lavoro di esempio con autenticazione basata su SSO del browser Web SAML {#sample-wf}

1. Il visualizzatore passa a un sito (dummy1.com) e tenta di accedere al contenuto autorizzato.
1. La pagina video/lettore carica l’Access Enabler da adobe.com e, quando richiesto dall’azione dell’utente, richiede l’autorizzazione per il contenuto richiesto.
1. Access Enabler esegue e convalida il richiedente e la richiesta.
1. Access Enabler verifica la presenza di un token di autorizzazione valido nell&#39;archivio locale. Se viene trovata un&#39;autorizzazione valida, Access Enabler produce un token multimediale di breve durata (vedere il passaggio 14).
1. Se non viene trovata alcuna autorizzazione valida per la risorsa richiesta ma esiste un token di autenticazione valido, Access Enabler avvia una richiesta di autorizzazione con il provider di servizi Pay TV su cui l&#39;utente è autenticato. Il server di Adobe esegue lo scambio di richieste di autorizzazione/risposte con il provider di servizi di televisione a pagamento.
1. Se non viene trovato alcun token di autenticazione valido, Access Enabler richiede all&#39;utente di specificare il proprio provider di Pay TV. Se si seleziona un provider che supporta l’autenticazione basata su SSO del browser web SAML, viene attivato un flusso di lavoro di autenticazione basato su SAML. Per i provider non SAML, Adobe gestisce un flusso di lavoro personalizzato simile.)
1. Access Enabler passa al browser per il servizio SAML SP (Service Provider) di Adobe, trasmettendogli tutti i parametri appropriati.
1. L&#39;SP SAML richiama l&#39;IDP (Identity Provider) SAML appropriato presso il provider di Pay TV dell&#39;utente, utilizzando il profilo del browser Web SAML indicato nei metadati IdP. In questo modo l’utente viene indirizzato al sito dell’IdP (provider di Pay TV), dove si autentica.
1. Dopo aver eseguito correttamente l’autenticazione, l’utente viene reindirizzato all’SP SAML di Adobe, trasmettendogli un GUID di autenticazione nella risposta SAML.
1. Adobe SAML SP crea una sessione sul lato server in cui è memorizzato il GUID di autenticazione e reindirizza l&#39;utente alla pagina Programmatore originale. La sessione del server viene eliminata al recupero del token authN da parte di Access Enabler.
1. Access Enabler recupera il GUID di autenticazione dal server Adobe per includerlo nel token con un ID dispositivo gestito dall’autenticazione Adobe Primetime. Quando DRM di Flash si trova sul dispositivo, ciò viene effettuato tramite API di Flash Access (componente DRM del Flash Player) che abilitano l&#39;associazione del GUID all&#39;ID dispositivo e restituiscono un token di autenticazione. In caso contrario, l’operazione viene eseguita tramite API JS su HTTPS utilizzando l’archiviazione basata su HTML5 o tramite componenti nativi specifici.
1. Il token di autenticazione viene utilizzato da Access Enabler per effettuare richieste di autorizzazione al provider di Pay TV. Sui dispositivi abilitati per il Flash Access, le richieste vengono sempre effettuate tramite API di Flash Access in modo che il token di autorizzazione risultante sia associato al dispositivo. Sui dispositivi non di Flash Access, HTTPS viene utilizzato per la comunicazione protetta tra client e server.
1. Se l’autorizzazione ha esito positivo, Adobe Primetime crea un token di autorizzazione di lunga durata (&quot;authZ&quot;) e lo trasmette all’Access Enabler, che lo memorizza sul sistema locale.
1. L’Access Enabler utilizza il token authZ per creare token multimediali di breve durata utilizzati per l’accesso effettivo alla visualizzazione. Per motivi di sicurezza, questi token di breve durata devono essere convalidati da un altro componente di autenticazione Adobe Primetime, Media Token Verifier.

![](assets/authn-authz-entitlmnt-flow.png)


*Figura 4: flusso di lavoro di Authentication and authorization Access Enabler*

##### Interfaccia utente di adesione {#entitlement-ui}

I programmatori devono creare la propria interfaccia utente per il flusso di lavoro di accesso nel proprio sito web o app. Alcuni elementi, come la procedura di accesso effettiva, sono forniti dal provider di Pay TV e alcuni elementi sono facoltativamente disponibili come parte dell’autenticazione di Adobe Primetime. Come minimo, il programmatore esegue le seguenti operazioni:

* **Implementa un’interfaccia di selezione del provider** che consente a un nuovo utente di identificare il proprio provider di Pay TV ed effettuare il primo accesso. Per lo sviluppo, Access Enabler fornisce un&#39;interfaccia utente di base che offre al cliente la possibilità di scegliere tra provider di servizi di televisione a pagamento e avvia il processo di accesso. Per un ambiente di produzione, i programmatori devono implementare una propria finestra di dialogo del selettore del provider. Alcuni provider di Pay TV reindirizzano al proprio sito per l&#39;accesso e altri richiedono che le pagine di accesso vengano visualizzate in un iframe. I programmatori devono implementare il callback che crea questo iframe, nel caso in cui il cliente scelga uno di questi provider.
* **Identifica le risorse protette.** Le risorse protette sono quelle che richiedono l’autorizzazione di accesso. Nell’offrire queste risorse, l’interfaccia del programmatore deve indicare la necessità di un’autorizzazione prima della visualizzazione. Se l’autorizzazione viene eseguita correttamente, l’interfaccia dovrebbe indicare che la risorsa è ora autorizzata.
* **Crea e gestisce un elenco di provider di Pay TV** per controllare l&#39;accesso degli utenti solo ai provider specificati.
* **Mostra che un utente è autenticato.** Il programmatore deve indicare lo stato di autenticazione del cliente come parte dei mezzi utilizzati per identificare le risorse protette. I programmatori possono eseguire query sull&#39;attivatore di accesso per determinare se un cliente è già stato autenticato.

#### Supporto di disconnessione singola {#single-logout-support}

Nella maggior parte dei casi, il programmatore è responsabile della gestione dei loghi utente tramite una semplice chiamata API. La chiamata logout() indica all’autenticazione Primetime di disconnettersi dall’utente corrente:

* Eliminazione di tutti i token AuthN e AuthZ
* Cancellazione di tutte le informazioni di autenticazione e autorizzazione per l&#39;utente
* Avvio di un flusso di lavoro specifico per il provider di Pay TV per cancellare la sessione di autenticazione dell&#39;utente con il provider (ad esempio, se l&#39;autenticazione è stata eseguita utilizzando il protocollo di richiesta di autenticazione SAML, la disconnessione può essere eseguita utilizzando il protocollo di disconnessione singola SAML).

Se l&#39;utente lascia il computer inattivo per un tempo sufficiente a far scadere i token, può comunque tornare alla sessione e avviare correttamente la disconnessione. L’autenticazione Adobe Primetime assicura che tutti i token vengano eliminati e avvisa il provider di Pay TV di eliminare anche la propria sessione.


Quando la disconnessione viene avviata da un sito che non è integrato con l&#39;autenticazione Adobe Primetime, il provider di Pay TV può richiamare il servizio di autenticazione Adobe Primetime Single Logout tramite un reindirizzamento del browser.

## Oltre ai flussi di adesione di base - Caratteristiche aggiuntive {#beyond-basics}

I flussi di adesione di base sono Avvio, Autenticazione, Autorizzazione e Disconnessione.  Con la maturazione e lo sviluppo dell’autenticazione Adobe Primetime, sono state e vengono aggiunte ai flussi di base diverse funzioni aggiuntive.  Tra questi:

* **Metadati utente** - In base agli accordi tra MVPD e programmatori, gli MVPD possono scambiare in modo sicuro metadati quali codice postale, valutazione massima, ID canale e altro ancora. I metadati consentono diversi casi d’uso, tra cui controllo dei genitori, periodi di blocco regionali per eventi sportivi, ecc.
* **Accesso gratuito temporaneo** - Consente ai programmatori di offrire un accesso gratuito temporaneo ai loro contenuti protetti (ad esempio, brevi esempi di programmazione giornaliera o la presentazione gratuita di un evento di grandi dimensioni).
* **MVPD proxy** - Un MVPD può gestire la propria integrazione con l’autenticazione Adobe Primetime, nonché il processo di adesione per conto di un gruppo di &quot;ProxiedMVPDs&quot; associati.

## Sicurezza {#security}

In questa sezione vengono evidenziate la sicurezza e l’integrità dell’infrastruttura di autenticazione di Adobe Primetime.

### Sicurezza dei token {#token-security}

Uno degli obiettivi principali dell’autenticazione di Adobe Primetime è garantire che il sistema possa resistere agli attacchi ai dati di adesione ai contenuti da parte di un utente malintenzionato o di un aggregatore di contenuti. L’accesso ai dati è pertanto protetto a diversi livelli nel flusso di lavoro, proteggendo la generazione e l’utilizzo dei dati del token di autorizzazione con la massima importanza. L’architettura di autenticazione di Adobe Primetime è progettata per garantire che i contenuti dei token siano mantenuti in modo sicuro e che il token rimanga sul dispositivo a cui è stato rilasciato.

* **Sicurezza dei token AuthN e AuthZ di lunga durata** : tutti i token a lunga durata dispongono di una firma digitale apposta dal server di autenticazione di Adobe Primetime. La firma digitale, tuttavia, differisce da piattaforma a piattaforma, in quanto utilizza un ID dispositivo che differisce nelle modalità di generazione, protezione e convalida. In tutti i casi, una convalida lato client garantisce che la firma digitale sia intatta e che l’integrità del token sia preservata. Access Enabler memorizza in modo sicuro i token convalidati nelle posizioni specifiche dell’ambiente in cui è in esecuzione. Se la convalida dell’ID dispositivo non riesce, la sessione di autenticazione viene invalidata, i token vengono reimpostati e all’utente viene richiesto di effettuare di nuovo l’accesso.
* **Protezione token multimediale di breve durata** - I token multimediali di breve durata, prodotti nella fase finale prima dell&#39;accesso ai contenuti, sono firmati da un Adobe e crittografati per evitare manomissioni durante lo scambio. I token multimediali di breve durata richiedono anche un ulteriore passaggio di convalida da parte di un componente di autenticazione Adobe Primetime aggiuntivo, Media Token Verifier. Il TTL del token di breve durata è impostato sul valore predefinito di 5 minuti e può essere abbreviato, se necessario. Il token Media di breve durata non viene mai memorizzato nella cache; un nuovo token viene recuperato dal server ogni volta che viene chiamata un’API di autorizzazione.

### Sicurezza dei dispositivi specifica per la piattaforma {#platform-sp-security}

Le misure di sicurezza utilizzate dall’autenticazione Adobe Primetime variano a seconda della piattaforma, ma sono tutte affidabili e all’avanguardia.

* **Dispositivi abilitati per il Flash** - Quando il Flash Player 10.1+ o AIR 2.5+ si trova sul dispositivo, l’autenticazione Adobe Primetime utilizza la funzionalità DRM di Flash Player per la protezione, nota anche come Flash Access. Il Flash offre un ulteriore livello di protezione; la forte garanzia del binding dei dispositivi per i token basati su Flash significa che, nella maggior parte dei casi, il time-to-live può essere più lungo, l’utente non deve accedere così spesso e l’esperienza utente è generalmente più fluida.
* **Esperienze nel browser su dispositivi compatibili con HTML5**- Sui dispositivi non di Flash che includono la funzionalità di browser HTML5, l’autenticazione Adobe Primetime dispone di un mezzo alternativo di protezione limitata per le integrazioni basate su browser. Tuttavia, poiché il binding del dispositivo per HTML5 non è altrettanto forte, il time-to-live (TTL) per i token sulle piattaforme HTML5 è in genere più breve.
* **Supporto di app native per dispositivi in casa e fuori casa** - Adobe offre SDK nativi per sistema operativo (iOS, Android, Windows 8, ecc.) che forniscono maggiore sicurezza rispetto alla soluzione HTML5. Questi SDK utilizzano API native per recuperare un ID dispositivo e trasmetterlo in modo sicuro al server di autenticazione di Adobe Primetime.
* **Clientless** - L’autenticazione Adobe Primetime utilizza il protocollo HTTPS per garantire una comunicazione sicura. Inoltre, tutte le chiamate provenienti da uno smart device devono essere firmate digitalmente.

## Domande frequenti {#faqs}

**Che cos&#39;è TV Everywhere?**
Il movimento di settore noto come TV Everywhere consente ai clienti di pay TV di accedere ai contenuti premium a cui si abbonano già su una varietà di dispositivi connessi a Internet, tra cui personal computer, tablet, smartphone, console di giochi, set-top box e TV &quot;Smart&quot;. La sfida di questa iniziativa è rendere il processo di autenticazione il più semplice e indolore possibile, consentendo ai clienti di accedere senza problemi ai contenuti dell’abbonamento senza barriere proibitive e con più accessi.


**Cos’è l’autenticazione Adobe Primetime e come si relaziona con TV Everywhere?**
L’autenticazione Adobe Primetime porta TV Everywhere dal concetto alla realtà verificando agevolmente il diritto di un utente al contenuto in modo semplice e sicuro. L’autenticazione Adobe Primetime è un servizio ospitato che consente una rapida integrazione back-end basata sulle regole di business richieste sia dai programmatori che dai provider di Pay TV. Ciò significa tempi di commercializzazione rapidi per tutte le parti, un ambiente più sicuro per prevenire le frodi e una migliore esperienza del cliente, con più contenuti TV disponibili per più persone su più piattaforme.


**Come viene offerta/fornita l’autenticazione Adobe Primetime?**
L’autenticazione Adobe Primetime è offerta tramite il modello SaaS (Software as a Service). Ciò consente una comunicazione più sicura tra gli utenti finali, i programmatori e i fornitori di servizi di televisione a pagamento al fine di convalidare il diritto ai contenuti. I componenti core del servizio includono l’Access Enabler lato client (o l’API senza client per alcuni dispositivi) e il server di autenticazione Adobe Primetime in hosting. L&#39;Access Enabler è un file di piccole dimensioni caricato nella pagina Web o nell&#39;applicazione di un programmatore. Comunica con i server di autenticazione di Adobe Primetime, che a loro volta dispongono di connessioni integrate nei sistemi di autenticazione di vari provider di Pay TV. L’autenticazione Adobe Primetime offre anche un approccio API senza client all’integrazione per alcuni &quot;dispositivi avanzati&quot; che non sono compatibili con il web (Smart TV, set-top box, console giochi, ecc.). L’approccio Clientless fornisce servizi web RESTful con cui gli sviluppatori possono implementare i flussi di autenticazione di Adobe Primetime su questi dispositivi.


**Quali sono le differenze tra l’autenticazione di Adobe Primetime e le altre soluzioni TV Everywhere?**
L’autenticazione Adobe Primetime offre vantaggi significativi rispetto alle soluzioni alternative di TV Everywhere. Le integrazioni dirette con singoli provider non forniscono la flessibilità di un accesso singolo e permanente (SSO), in quanto gli utenti si spostano da un sito all’altro attraverso Internet. L&#39;autenticazione Adobe Primetime ha anche una notevole penetrazione di mercato; una volta che un programmatore si integra con l&#39;autenticazione Adobe Primetime, sono immediatamente connessi con gli operatori di Pay TV che servono oltre il 90% delle famiglie negli Stati Uniti. Inoltre, l’autenticazione Adobe Primetime sfrutta funzioni di sicurezza univoche integrate nel runtime di Flash (ove disponibile) per attenuare le frodi, fornendo al contempo SDK che consentono ai programmatori di disporre della stessa funzionalità TV Everywhere incorporata nelle app native per dispositivi mobili o domestici in cui il Flash non è disponibile. Infine, anche se l’autenticazione Adobe Primetime è disponibile come servizio indipendente, offriamo anche la possibilità di una stretta integrazione con altri prodotti e servizi Adobi (tra cui Primetime e Adobe Analytics) relativi alla distribuzione, alla protezione e alla monetizzazione dei contenuti TV Everywhere.

**Quanto è sicura l’autenticazione Adobe Primetime?**
La priorità numero uno dell’architettura di autenticazione di Adobe Primetime è garantire che solo i visualizzatori autorizzati siano autenticati e abbiano accesso ai contenuti premium. L’autenticazione Adobe Primetime associa strettamente l’accesso al dispositivo di visualizzazione e può aiutare a limitare flussi, sessioni e/o dispositivi per una determinata famiglia.


**È necessario specificare un Flash Player?**
Il Flash Player Adobe 11.x o successivo è richiesto per la sicurezza di associazione del dispositivo più rigida. Tuttavia, l’autenticazione Adobe Primetime per TV Everywhere è indipendente dal lettore e dalla piattaforma, e si integra con qualsiasi applicazione di riproduzione, inclusi Silverlight e HTML5. Inoltre, l&#39;autenticazione Adobe Primetime fornisce supporto nativo per dispositivi come iOS, Android e Xbox in cui il Flash Player non è disponibile.  Infine, l’autenticazione Adobe Primetime fornisce un approccio senza client per i dispositivi che non sono in grado di eseguire il rendering di una pagina web (console di giochi, Smart TV, set-top box).


**Quali dispositivi sono supportati dall’autenticazione Adobe Primetime?**
L’autenticazione Adobe Primetime è supportata praticamente da qualsiasi dispositivo con il kit web HTML5 per le esperienze di visualizzazione nel browser. Inoltre, l’autenticazione Adobe Primetime continua a distribuire kit di sviluppo software nativi (SDK) per varie piattaforme specifiche per dispositivi, tra cui iOS, Android™ e Windows 8. L’autenticazione Adobe Primetime supporta parzialmente alcuni dispositivi non compatibili con il web (Smart TV, set-top box, console di gioco, ecc.) tramite le API dei servizi web RESTful.

**L’autenticazione Adobe Primetime supporta gli standard emergenti per TV Everywhere?**
L’autenticazione di Adobe Primetime è conforme alla **CableLabs OLCA (accesso ai contenuti online)** [specifica](https://www.cablelabs.com/specifications), che fornisce i requisiti tecnici e l&#39;architettura per la distribuzione di video a un cliente di Pay TV da fonti online. Adobe ha partecipato al progetto congiunto di test di interoperabilità CableLabs nel giugno 2011 e ha superato il processo di test per un&#39;implementazione di Service Provider. L’autenticazione Adobe Primetime viene verificata (completa e testata) in base alle specifiche OLCA per l’autenticazione. Il componente di autorizzazione è completato, ma la verifica dei test attende il rilascio dell&#39;ambiente di test di CableLabs (ETA Nov 2011).

L’Adobe è anche un membro attivo del **OATC (Open Authentication Technical Consortium, consorzio tecnico per l’autenticazione aperta)** e partecipa a numerosi progetti di elaborazione di specifiche dei sottocomitati in quanto parte di tale organismo.

**In che modo l’autenticazione Adobe Primetime gestisce la gestione federated identity management/single sign-on (SSO)?**
L’autenticazione Adobe Primetime ti consente di fornire ai clienti l’autenticazione e l’autorizzazione Single Sign-On (SSO), utilizzando la comunicazione back-channel (server-to-server) tra l’autenticazione Adobe Primetime e gli operatori Pay TV partecipanti. Quindi, con l’autenticazione Adobe Primetime, non è necessario che gli abbonati effettuino nuovamente l’accesso dopo la prima autenticazione, fino a quando quest’ultima è consentita dall’operatore di Pay TV per persistere. In genere questo limite è impostato su 30 giorni. A tal fine, l’autenticazione Adobe Primetime fornisce ai clienti un dominio comune per i token di autenticazione. Queste informazioni sullo stato di autenticazione sono disponibili per tutti i siti partecipanti che sono integrati con un determinato operatore di Pay TV.

Attualmente, la maggior parte delle integrazioni di autenticazione Adobe Primetime con gli operatori di Pay TV utilizza il protocollo SAML, uno degli standard di autenticazione primari. L’autenticazione Adobe Primetime funge da provider di servizi proxy nell’architettura SAML e mantiene la risposta di autenticazione SAML come token protetto nel dominio comune di Adobe. L’autenticazione di Adobe Primetime è conforme a SAML 2.0.

Anche se a questo punto l&#39;autenticazione Adobe Primetime viene tipicamente utilizzata con le soluzioni SAML SSO, l&#39;architettura di autenticazione Adobe Primetime astrae tutte le specifiche di protocollo dall&#39;integrazione del programmatore. Pertanto, è possibile aggiungere nel tempo il supporto di nuovi protocolli, come quelli basati su OAuth 2.0 o su protocolli personalizzati.

**Quanto costa l&#39;autenticazione Adobe Primetime per TV Everywhere agli utenti finali?**
L’utilizzo dell’autenticazione Adobe Primetime non comporta costi aggiuntivi per gli utenti finali.

>[!NOTE]
>
>**Passaggi successivi:** Per ulteriori informazioni, contatta il rappresentante del tuo Adobe o compila il modulo di richiesta di informazioni [qui](https://www.adobe.com/cfusion/mmform/index.cfm?name=adobepass_rfi).
