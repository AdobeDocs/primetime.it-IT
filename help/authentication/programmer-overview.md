---
title: Panoramica per programmatori
description: Panoramica per programmatori
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---


# Panoramica Per I Programmatori {#programmers-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#introduction}

Questa panoramica è destinata al provider di contenuti (programmatore) che intende integrare Adobe® Pass nel proprio sito web o applicazione. Per ulteriore documentazione, incluse le guide all&#39;integrazione e Kickstart, consulta Informazioni correlate di seguito.

Oggi i tuoi spettatori possono accedere a Internet in qualsiasi momento, ovunque e richiedere l&#39;accesso ai contenuti protetti direttamente da te, il Programmatore. Potrebbero voler guardare un evento una tantum, o cercare i diritti di visualizzazione di un&#39;intera serie televisiva che stai trasmettendo.

Ma prima di consentire l’accesso ai contenuti protetti, è necessario determinare se un cliente ha il diritto di visualizzarli. Dispongono di un abbonamento con un distributore di programmazione video multicanale (MVPD)? In caso affermativo, l&#39;abbonamento include la programmazione?

Determinare l&#39;adesione di un visualizzatore non è sempre semplice per un programmatore. Gli MVPD detengono i dati identificativi e i privilegi di accesso per i loro clienti.  Aggiungete il fatto che i visualizzatori che cercano di accedere ai contenuti protetti si abbonano a una varietà di MVPD, ciascuno dei quali ha sistemi diversi, ed è facile vedere che determinare l&#39;adesione del visualizzatore ai contenuti protetti può rapidamente diventare complicato e tecnicamente impegnativo:

![](assets/user-ent-by-progr.png)

*Figura: Autorizzazione Utente Determinata Direttamente Dal Programmatore*

L&#39;autenticazione Adobe Primetime per TV Everywhere media in modo sicuro queste transazioni di adesione tra programmatori e MVPD. L’autenticazione Adobe Primetime consente ai programmatori di fornire contenuti protetti a clienti validi in modo semplice, rapido e sicuro:

![](assets/user-ent-mediatedby-authn.png)

*Figura: Autorizzazione utente Mediata dall’autenticazione Adobe Primetime*

L’autenticazione Adobe Primetime funge da proxy negli scambi con gli MVPD partecipanti, in modo da poter presentare ai visualizzatori un’interfaccia coerente tra siti diversi. L’autenticazione Adobe Primetime consente inoltre di fornire ai visualizzatori autenticazione e autorizzazione single sign-on (SSO). L’autenticazione e l’autorizzazione vengono tracciate per tutti i servizi partecipanti, in modo che un utente iscritto non debba effettuare nuovamente l’accesso dopo la prima autenticazione sul proprio sistema.

* **Autenticazione** - Il processo di conferma con un MVPD che un dato utente è un cliente noto.
* **Autorizzazione** - Il processo di conferma con un MVPD che un utente autenticato ha una sottoscrizione valida a una risorsa specificata.

### Funzionamento dell’autenticazione Adobe Primetime {#HowItWorks}

L&#39;applicazione per la visualizzazione dei contenuti del programmatore interagisce con l&#39;autenticazione Adobe Primetime utilizzando il componente client di Access Enabler o i servizi web RESTful dell&#39;API Clientless (per dispositivi non adatti al web come smart TV, console giochi, set-top box, ecc.). Access Enabler viene eseguito sul sistema dell&#39;utente, in cui facilita tutti i flussi di lavoro di adesione.  Il componente Access Enabler viene scaricato dal suo sito di hosting all&#39;Adobe quando i clienti accedono al tuo sito e richiedono contenuto protetto.  I server di autenticazione Adobe Primetime ospitano i servizi web RESTful utilizzati nella soluzione Clientless.

L’autenticazione Adobe Primetime gestisce i flussi di lavoro di adesione effettivi fornendo al contempo le primitive utilizzate per:

* Imposta la tua identità. (Il programmatore è il &quot;richiedente&quot; nel flusso di adesione all&#39;autenticazione di Adobe Primetime.)
* Autentica un utente con un particolare MVPD.  (L&#39;MVPD è il &quot;provider di identità&quot; o &quot;IdP&quot; nel flusso di adesione all&#39;autenticazione di Adobe Primetime.)
* Autorizza un utente con MVPD per una particolare risorsa.
* Esci dall’utente.

Il programmatore è responsabile della pagina Web o dell&#39;applicazione di livello superiore che esegue le seguenti operazioni:

* Implementa l’interfaccia utente
* Interagisce con i servizi web di Access Enabler o senza client API

L&#39;obiettivo dell&#39;autenticazione Adobe Primetime è quello di creare un modo semplice e modulare per i programmatori e gli MVPD per gestire la verifica dell&#39;adesione.

## Informazioni sui token {#understanding-tokens}

La soluzione di adesione all&#39;autenticazione di Adobe Primetime si basa sulla generazione di parti specifiche di dati che vengono create al completamento dei flussi di lavoro di autenticazione e autorizzazione. Questi dati sono chiamati token. I gettoni hanno una durata di vita limitata; al momento della scadenza, i token devono essere riemessi mediante il riavvio dei flussi di lavoro di autenticazione e autorizzazione.

Per informazioni dettagliate sui token, consulta le sezioni seguenti:

* [Tipi di token](#token-types)
* [Archiviazione token](#token-storage)
* [Sicurezza dei token](#token-security)
* [Condivisione token](#token-sharing)

### Tipi di token {#token-types}

Durante i flussi di lavoro di autenticazione e autorizzazione vengono rilasciati tre tipi di token. I token AuthN e AuthZ sono &quot;longevi&quot; e offrono continuità nell’esperienza visiva dell’utente. Media Token è un token di breve durata che fornisce supporto per le best practice del settore per prevenire le frodi attraverso la rimozione dei flussi. I programmatori specificano i valori TTL (time-to-live) per ogni tipo di token in base agli accordi conclusi con MVPD. I programmatori decidono un valore TTL che meglio si adatta alla tua azienda e ai tuoi clienti.

* **Token AuthN** (&quot;Lunga vita&quot;): Dopo l’autenticazione, Adobe Primetime Authentication crea un token AuthN associato sia al dispositivo richiedente che a un identificatore univoco globale (GUID).
   * L’autenticazione Adobe Primetime invia il token AuthN ad Access Enabler, che lo memorizza in cache in modo sicuro sul sistema del client.  Il token AuthN è presente e non è scaduto, ma è disponibile per tutte le applicazioni che utilizzano l’autenticazione Adobe Primetime. Access Enabler utilizza il token AuthN per il flusso di autorizzazione.
   * In qualsiasi momento viene memorizzato nella cache un solo token AuthN. Ogni volta che viene emesso un nuovo token AuthN e ne esiste già uno vecchio, l’autenticazione Adobe Primetime sovrascrive il token memorizzato nella cache.
* **Token AuthZ** (&quot;Lunga vita&quot;): Dopo l’autorizzazione, l’autenticazione Adobe Primetime crea un token AuthZ associato al dispositivo richiedente e a una risorsa protetta specifica.  La risorsa protetta è identificata da un ID di risorsa univoco.
   * L’autenticazione Adobe Primetime invia il token AuthZ ad Access Enabler, che lo memorizza in cache in modo sicuro sul sistema locale. Access Enabler utilizza quindi il token AuthZ per creare il token Media di breve durata utilizzato per l&#39;accesso effettivo alla visualizzazione.
   * In qualsiasi momento viene memorizzato nella cache un solo token AuthZ per risorsa. L’autenticazione Adobe Primetime può memorizzare nella cache più token AuthZ, purché siano associati a risorse diverse. Ogni volta che viene emesso un nuovo token AuthZ e ne esiste già uno vecchio per la stessa risorsa, l’autenticazione Adobe Primetime sovrascrive il token memorizzato nella cache.
* **Token multimediale** (&quot;a vita breve&quot;): Access Enabler utilizza il token AuthZ per generare una breve durata (impostazione predefinita: 7 minuti) Token multimediale. Questo è il punto in cui si ritiene che si sia verificata una richiesta di riproduzione corretta.
   * Prima di fornire l’accesso alla risorsa protetta, il server multimediale deve utilizzare un componente di autenticazione di Adobe Primetime, il Verificatore dei token multimediali, per convalidare il token multimediale.
   * Poiché il token multimediale non è associato al dispositivo, la sua durata è significativamente più breve (impostazione predefinita: 7 minuti) rispetto a quelli dei token AuthN e AuthZ di lunga durata.
   * Il token per contenuti multimediali di breve durata è limitato all’utilizzo una tantum e non viene mai memorizzato nella cache. Viene recuperato dal server di autenticazione di Adobe Primetime ogni volta che viene chiamata un’API di autorizzazione.

### Archiviazione token {#token-storage}

Access Enabler memorizza token di lunga durata (AuthN e AuthZ) in luoghi specifici per il proprio ambiente:

* **Flash 10.1** (o superiore): I token longevi vengono memorizzati come oggetti condivisi locali.
* **HTML5**: I token di lunga durata vengono conservati in modo sicuro nel negozio locale del browser HTML5.
* **iOS**: I token longevi vengono memorizzati su un tavolo di montaggio permanente, dove è possibile accedervi da altre applicazioni client di autenticazione Adobe Primetime.
* **Android**: I token longevi vengono archiviati in un file di database condiviso, a cui è possibile accedere da altre applicazioni client di autenticazione Adobe Primetime.
* **Dispositivi API senza client**: I token sono memorizzati sui server di autenticazione Primetime.

### Sicurezza dei token {#token-security}

Adobe Primetime Authentication Server firma digitalmente tutti i token longevi utilizzando l&#39;ID dispositivo (derivato dalle caratteristiche hardware del dispositivo). La firma digitale varia a seconda dell’ambiente in cui viene generata, protetta e convalidata:

* **Flash 10.1** (o superiore): l&#39;ID dispositivo si basa sulla credenziale del dispositivo, un certificato univoco rilasciato dal server di Individualizzazione di Adobe. Questa sicurezza equivale alla tecnologia DRM FAXS. Questa convalida lato server confronta l’ID dispositivo univoco nel token con la credenziale del dispositivo (comunicata in modo sicuro dall’autenticazione Flash Player ad Adobe Primetime). Le credenziali del dispositivo identificano anche la versione client FAXS e la versione del Flash Player (o AIR) a cui è stata rilasciata. Il binding del dispositivo è più forte rispetto a HTML5, pertanto il time-to-live (TTL) per i token è in genere più lungo con il Flash.
* **HTML5** - Il dispositivo è personalizzato sul lato client. Utilizza le caratteristiche disponibili in JavaScript per produrre un ID pseudo-dispositivo che include versioni del browser e del sistema operativo, un indirizzo IP e un GUID cookie del browser (identificatore univoco globale). Questo ID dispositivo token viene confrontato con l&#39;ID pseudo-dispositivo corrente per il dispositivo. Poiché l’indirizzo IP può cambiare durante il normale utilizzo, anche nella stessa sessione, Adobe Primetime Authentication memorizza i token HTML5 in due posizioni: localStorage e sessionStorage. Se l&#39;IP cambia e il token sessionStorage è comunque valido, la sessione viene mantenuta. Con HTML5, il binding del dispositivo non è così forte, pertanto il TTL per i token è in genere più breve rispetto al Flash.
* **Client nativi** (iOS e Android) - I token longevi contengono informazioni native sull’individualizzazione degli ID dispositivo e sono quindi associati al dispositivo richiedente. Le richieste di autenticazione e autorizzazione vengono inviate tramite HTTPS e le informazioni sull’ID dispositivo vengono firmate digitalmente dalla libreria di Access Enabler prima di inviarle ai server di back-end. Sul lato server, le informazioni dell’ID dispositivo vengono convalidate in base alla firma digitale associata.
* **Client API senza client** - La soluzione API Clientless dispone di un set di protocolli di sicurezza che richiedono la firma digitale di tutte le chiamate API. I token generati durante i flussi di adesione vengono memorizzati in modo sicuro sui server di autenticazione di Adobe Primetime.

L’autenticazione Adobe Primetime convalida ogni token a lunga vita per garantire che il dispositivo che accede al contenuto sia lo stesso che ha rilasciato il token. Per tutti i token, una convalida lato client assicura che la firma digitale sia intatta e che l’integrità del token sia preservata. Quando la convalida dell’ID dispositivo non riesce, la sessione di autenticazione viene invalidata e all’utente viene richiesto di effettuare di nuovo l’accesso, il che reimposta i token.

### Condivisione token {#token-sharing}

Le applicazioni su piattaforme diverse non condividono token. Questo è dovuto a diversi motivi, tra cui i seguenti:

* Come descritto in [Archiviazione token](#token-storage), il metodo di memorizzazione dei token varia a seconda delle piattaforme (ad Flash, Oggetti condivisi locali, WebStorage per JavaScript).
* Il livello di sicurezza del token è diverso tra le piattaforme. Ad esempio, i token di Flash sono fortemente associati a un dispositivo che utilizza FAXS. I token in un ambiente JavaScript puro non hanno lo stesso livello di supporto DRM del Flash.  La condivisione di token JS con applicazioni di Flash aumenterebbe la possibilità di token meno sicuri che sfruttino un ambiente più sicuro.

## Ciclo di vita dell&#39;integrazione dei programmatori {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*Figura: Integrazione dell&#39;autenticazione con il sito web e l&#39;applicazione del programmatore*


## Flussi logici {#logical-flows}

### Diagramma di flusso di adesione {#chart}

Il seguente diagramma di flusso presenta il processo complessivo di conferma dell&#39;adesione (utilizzando il componente client di Adobe Primetime Authentication Access Enabler ):

![](assets/ent-flowchart.png)

*Figura: Processo di conferma del diritto*

### Passaggi di autenticazione {#authn-steps}

I passaggi seguenti presentano un esempio del flusso di autenticazione dell’autenticazione di Adobe Primetime.  Questa è la parte del processo di adesione in cui un programmatore determina se l&#39;utente è un cliente valido di un MVPD.  In questo scenario, l&#39;utente è un abbonato valido a un MVPD.  L&#39;utente sta tentando di visualizzare il contenuto protetto utilizzando un&#39;applicazione di Flash del programmatore:

1. L&#39;utente passa alla pagina Web del programmatore, che carica l&#39;applicazione del Flash del programmatore e i componenti di Adobe Primetime Authentication Access Enabler sul computer dell&#39;utente. L&#39;applicazione di Flash utilizza Access Enabler per impostare l&#39;identificazione del programmatore con l&#39;autenticazione Adobe Primetime, e l&#39;autenticazione Adobe Primetime fornisce ad Access Enabler i dati di configurazione e stato per quel programmatore (il &quot;richiedente&quot;). Access Enabler deve ricevere questi dati dal server prima di eseguire qualsiasi altra chiamata API. Nota tecnica: il programmatore imposta la propria identità con Access Enabler `setRequestor()` metodo; per ulteriori informazioni, consulta la [Guida all&#39;integrazione dei programmatori](/help/authentication/programmer-integration-guide-overview.md).
1. Quando l&#39;utente tenta di visualizzare il contenuto protetto del programmatore, l&#39;applicazione del programmatore presenta all&#39;utente un elenco di MVPD, da cui l&#39;utente seleziona un provider.
1. L’utente viene reindirizzato a un server di autenticazione Adobe Primetime, dove un [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) viene creata la richiesta per l&#39;MVPD selezionato dall&#39;utente. Questa richiesta viene inviata come richiesta di autenticazione per conto del programmatore al MVPD. A seconda del sistema MVPD, il browser dell&#39;utente viene quindi reindirizzato al sito MVPD per l&#39;accesso, oppure viene creato un iFrame di accesso nell&#39;app del programmatore.
1. In entrambi i casi (reindirizzamento o iFrame), l&#39;MVPD accetta la richiesta e visualizza la pagina di login.
1. L&#39;utente accede con l&#39;MVPD, l&#39;MVPD convalida lo stato dell&#39;utente come cliente pagante, e poi l&#39;MVPD crea la propria sessione HTTP.
1. Quando l&#39;utente viene convalidato, l&#39;MVPD crea una risposta (SAML e crittografato) che l&#39;MVPD invia nuovamente all&#39;autenticazione Adobe Primetime.
1. L&#39;autenticazione Adobe Primetime riceve la risposta MVPD, vede che c&#39;è una sessione HTTP di autenticazione Adobe Primetime aperta, convalida la risposta SAML dall&#39;MVPD e reindirizza al sito del programmatore.
1. Il sito del programmatore viene ricaricato, Access Enabler viene ricaricato e il programmatore richiama di nuovo setRequestor() .  La seconda chiamata a setRequestor() è necessaria perché la configurazione corrente è cambiata. È ora presente un flag che informa l&#39;utente che un token AuthN è in attesa di essere generato sul server.
1. Access Enabler rileva che è in sospeso l&#39;autenticazione e richiede il token dal server di autenticazione Adobe Primetime. Il token viene recuperato dal server richiamando le funzionalità DRM del Flash Player.
1. Il token AuthN è memorizzato nella cache LSO di Flash Player del programmatore; l’autenticazione è ora completa e la sessione viene eliminata sul server di autenticazione Adobe Primetime.

### Passaggi di autorizzazione {#authz-steps}

I seguenti passaggi continuano da [Passaggi di autenticazione](#authn-steps):

1. Quando l&#39;utente tenta di accedere al contenuto protetto del programmatore, l&#39;applicazione del programmatore controlla prima un token AuthN sul computer o sul dispositivo locale dell&#39;utente.  Se il token non è presente, il [Passaggi di autenticazione](#authn-steps) sono seguite le indicazioni di cui sopra.  Se il token AuthN è presente, il flusso di autorizzazione procede con l&#39;applicazione del programmatore che avvia una chiamata a Access Enabler con una richiesta per ottenere i diritti di visualizzazione dell&#39;utente per un elemento specifico di contenuto protetto.
1. L’elemento specifico del contenuto protetto è rappresentato da un &quot;identificatore di risorsa&quot;.  Può trattarsi di una stringa semplice o di una struttura più complessa, ma in ogni caso la natura dell&#39;identificativo della risorsa è concordata in anticipo tra il programmatore e l&#39;MVPD.  L&#39;applicazione del programmatore passa l&#39;identificatore della risorsa a Access Enabler.  Access Enabler controlla la presenza di un token AuthZ nel computer o nel dispositivo locale dell&#39;utente.  Se il token AuthZ non è presente, Access Enabler trasmette la richiesta al server di autenticazione Adobe Primetime back-end.
1. Il server di autenticazione Adobe Primetime comunica con l’endpoint di autorizzazione MVPD utilizzando protocolli standardizzati.  Se la risposta dell&#39;MVPD indica che l&#39;utente ha il diritto di visualizzare il contenuto protetto, il server di autenticazione Adobe Primetime crea un token AuthZ e lo ritrasmette all&#39;Access Enabler, che memorizza il token AuthZ sul computer dell&#39;utente.
1. Con un token AuthZ memorizzato sul computer o sul dispositivo dell&#39;utente, l&#39;applicazione del programmatore chiama Access Enabler per ottenere un token multimediale dal server di autenticazione Adobe Primetime e fornisce tale token all&#39;applicazione del programmatore.
1. Infine, l’applicazione del programmatore utilizza il componente Media Token Verifier per confermare che l’utente corretto sta visualizzando il contenuto corretto e con il token multimediale attivo, l’utente può visualizzare il contenuto protetto.


## Registrazione e inizializzazione {#reg-and-init}

Il primo passaggio nell’utilizzo dell’autenticazione Adobe Primetime consiste nel registrarsi con Adobe o con un partner autorizzato per l’autenticazione di Adobe Primetime.

Quando ti registri, fornisci un elenco dei domini da cui comunicherai con l’autenticazione Adobe Primetime. Ad esempio, i domini Turner Broadcasting System includono tbs.com e tnt.tv come domini registrati per l’autenticazione Adobe Primetime. A ciascuno di questi siti di contenuto viene concesso l’accesso all’autenticazione Adobe Primetime e viene assegnato il proprio ID richiedente (ad esempio, &quot;TBS&quot; e &quot;TNT&quot;). Se decidi di aggiungere altri siti, devi informare Adobe dei nomi di dominio aggiuntivi per inserirli nell’elenco dei domini consentiti e ottenere ID di richiedenti aggiuntivi.

>[!WARNING]
>
>Durante il test dell&#39;integrazione, assicurati che il server di test si trovi su un dominio registrato che intendi utilizzare in produzione. Le richieste, anche le richieste di test, provenienti da domini non inseriti nella whitelist vengono ignorate. Ad esempio, se hai richiesto l’utilizzo di domain.com in produzione, assicurati di distribuire l’integrazione di test sotto domain.com, test.domain.com e staging.domain.com.
>
>Le richieste che contengono nome utente e/o password nell’URL vengono ignorate anche se i domini sono inseriti nella whitelist. Esempio: `//username@registered-domain/`

L’ID del richiedente identifica in modo univoco il client del programmatore in tutte le comunicazioni con il componente client Access Enabler di Adobe Primetime Authentication. Tutti i dati statici di autenticazione di Adobe Primetime associati al programmatore vengono collegati a questo ID.

>[!TIP]
>
>Oltre all’ID del richiedente, quando si registra si ricevono anche URL funzionali per il componente client di Access Enabler e il verificatore del token multimediale.

## Passaggi di integrazione {#integration-steps}

>[!TIP]
>
>Se utilizzi il Open Source Media Framework Adobe (&quot;OSMF&quot;) per lo sviluppo del lettore multimediale, il modo più rapido per utilizzare l’autenticazione Adobe Primetime è quello di integrare il plugin OSMF *(Obsoleto)* nel codice del lettore.
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [Configurazione del richiedente](#requestor)
1. [Gestione dell’autenticazione e dell’autorizzazione](#authn-authz)
1. [Disconnessione singola supportata](#ssl)

### 1. Configurazione del richiedente {#requestor}

#### 1 bis. Registrazione con Adobe

Il primo passo è quello di registrarsi con l&#39;Adobe o con un partner autorizzato per l&#39;autenticazione di Adobe Primetime.  Al momento della registrazione viene rilasciato uno o più identificatori univoci globali (GUID). Ogni GUID rilasciato è associato a un dominio da cui l’accesso è consentito all’autenticazione Adobe Primetime. Si passa un GUID (denominato ID richiedente) per il dominio richiedente per registrare l&#39;identità per ogni sessione in cui si interagisce con Access Enabler. Per maggiori dettagli, vedi [Registrazione e inizializzazione](#reg-and-init) nella Guida all&#39;integrazione dei programmatori.

#### 1 ter. Integrazione iniziale di Access Enabler

Il passaggio successivo consiste nell’integrare Access Enabler nell’app o nella pagina web del lettore multimediale esistente:

* È possibile incorporare la versione di Flash, `AccessEnabler.swf`, in un lettore video basato su Flash o puoi incorporarlo direttamente nel HTML della pagina web. È possibile comunicare con Access Enabler SWF in ActionScript o JavaScript. L’API di base è ActionScript, ma se preferisci lavorare con JavaScript, è disponibile una libreria wrapper completa da includere nelle pagine.
* Per gli ambienti non Flash, puoi:
   * Utilizza la versione HTML5/JavaScript AccessEnabler.js e comunica con essa tramite l&#39;API JavaScript
   * Utilizza l’estensione nativa AIR per l’autenticazione Adobe Primetime per combinare il codice nativo con le classi ActionScript integrate
   * Utilizzare una delle versioni client native della libreria di Access Enabler (iOS o Android)

### 2. Gestione dell&#39;autenticazione e dell&#39;autorizzazione {#authn-authz}

#### 2 bis. Comunicazione con Access Enabler

La comunicazione tra Access Enabler e la pagina web o l’app di riproduzione è asincrona. L&#39;applicazione chiama i metodi di Access Enabler e Access Enabler risponde tramite i callback registrati con la libreria di Access Enabler.

* Quando l&#39;applicazione effettua una richiesta di autorizzazione, Access Enabler avvia automaticamente una richiesta di autenticazione, se nel sistema locale non è già presente un token AuthN valido. Quando l’autenticazione ha esito positivo, il token AuthN dell’utente viene memorizzato localmente, in modo che non sia necessario eseguire nuovamente l’accesso. Se sono stati autenticati correttamente tramite l’autenticazione Adobe Primetime in qualsiasi altro contesto (ad esempio, tramite il sito web MVPD o con un programmatore diverso), Access Enabler ha accesso al token AuthN locale e non è necessaria un’autenticazione aggiuntiva.
* Quando un utente tenta di accedere al contenuto protetto, invia una richiesta di autorizzazione ad Access Enabler. Dopo aver verificato (o avviato) l&#39;autenticazione, Access Enabler contatta l&#39;MVPD (tramite il server di autenticazione di Adobe Primetime) per determinare se il cliente è autorizzato a visualizzare il contenuto protetto. L&#39;applicazione deve solo inviare la richiesta ad Access Enabler e quindi gestire la risposta (autorizzazione riuscita o non riuscita). Se l’autorizzazione ha esito positivo, nel sistema client viene memorizzato un token AuthZ.  Infine, la tua applicazione riceve un token Media di breve durata da utilizzare nella tua procedura di autorizzazione.

>[!NOTE]
>
>* L’autenticazione si verifica come scambio SAML, tra l’autenticazione Adobe Primetime come fornitore di servizi (SP) e l’MVPD come fornitore di identità (IdP).
>
>* L’autorizzazione utilizza uno scambio di servizi web back-channel (server-to-server) tra l’autenticazione Adobe Primetime (l’SP) e un MVPD (l’IdP).



#### 2 ter. Fornire Un’Interfaccia Utente Di Autorizzazione {#entitlement-ui}

Fornisci una tua interfaccia utente per l’accesso degli utenti ai contenuti. Alcuni elementi, come il processo di accesso effettivo, sono forniti dall’MVPD e alcuni elementi sono facoltativamente disponibili come parte dell’autenticazione Adobe Primetime. Come minimo, effettua le seguenti operazioni:

* **Implementare un&#39;interfaccia di selezione MVPD che consenta a un nuovo utente di identificare il proprio MVPD e di effettuare l&#39;accesso per la prima volta**. Per lo sviluppo, Access Enabler fornisce un&#39;interfaccia utente di base che offre al cliente una scelta di MVPD e avvia il processo di accesso. Per la produzione, è necessario implementare la finestra di dialogo Selettore MVPD personalizzata. Alcuni MVPD vengono reindirizzati al proprio sito per l&#39;accesso e alcuni richiedono che le pagine di accesso siano visualizzate all&#39;interno di un iFrame. È necessario implementare un callback che crea questo iFrame per gestire i casi in cui l’MVPD dell’utente visualizza la propria pagina di accesso in un iFrame.
* **Identificare il contenuto protetto**. Il contenuto protetto richiede l’autorizzazione per accedere. L’interfaccia deve indicare il contenuto protetto e il contenuto autorizzato.  Lo stato di autorizzazione è spesso indicato con le icone &quot;sbloccato&quot; e &quot;bloccato&quot;.
* **Mostra l&#39;autenticazione di un utente**. Indica lo stato di autenticazione di un utente come parte di qualsiasi mezzo utilizzato per identificare il contenuto protetto. È possibile eseguire una query su Access Enabler per determinare se il cliente è già stato autenticato.

#### 2 quater. Integrazione del verificatore del token multimediale {#int-media-token-ver}

È necessario integrare il componente Verifica token multimediali di autenticazione di Adobe Primetime nel server multimediale.  In questo modo il verificatore token esistente può riconoscere i token Media di breve durata forniti dall’autenticazione Adobe Primetime con un’autorizzazione riuscita. Il Media Token Verifier convalida i token multimediali come ultimo passaggio di sicurezza prima di fornire all’utente l’accesso al contenuto protetto. Ricevi la posizione da cui scaricare il Media Token Verifier quando effettui la registrazione con Adobe.

### 3. Supporto di disconnessione singola {#ssl}

Nella maggior parte dei casi, il lettore multimediale è responsabile della gestione degli accessi utente tramite una semplice API di Access Enabler. Quando si chiama logout(), Access Enabler esegue le seguenti operazioni:

* Disconnette l&#39;utente corrente
* Cancella tutte le informazioni di autenticazione e autorizzazione per l&#39;utente disconnesso
* Elimina tutti i token AuthN e AuthZ dal sistema locale dell’utente

Se l’utente lascia il computer inattivo abbastanza a lungo da far scadere i token, può comunque tornare alla sessione e avviare correttamente l’logout. L’autenticazione Adobe Primetime assicura che tutti i token vengano eliminati e notifica all’MVPD di eliminare anche la loro sessione.

Quando l’accesso viene avviato da un sito non integrato con l’autenticazione Adobe Primetime, l’MVPD può richiamare il servizio Single Logout di autenticazione Adobe Primetime tramite un reindirizzamento del browser.

## Informazioni sugli ID utente {#user-ids}

Concettualmente, ogni utente che avvia un flusso di adesione è associato a un singolo ID utente univoco.  Tuttavia, nel corso di un flusso di adesione, un ID utente può essere presentato in modi diversi, a seconda dell&#39;API da cui si ottiene l&#39;ID.

Il sessionGUID nel token multimediale breve è il modulo protetto dell’ID utente, disponibile tramite la chiamata sendTrackingData() .   In tutte le integrazioni correnti, si tratta di un GUID permanente per l’utente in più dispositivi e nel tempo, ma l’origine del GUID inizia con l’ID utente nella risposta SAML dal MVPD.   Tuttavia, alcuni MVPD potrebbero cambiare idea in futuro, e iniziare a inviare un GUID transitorio.  Se un programmatore vuole garantire che l&#39;ID utente di origine MVPD nella risposta AuthN sia persistente, dovrebbe organizzarlo nei loro accordi con gli MVPD.

Di seguito sono elencati i diversi modi in cui l’ID utente viene rappresentato nelle API di autenticazione di Adobe Primetime:

* `sendTrackingData()` Proprietà GUID - Adobe di versione con hash dell&#39;ID utente MVPD.  Viene eseguito l’hashing in modo che l’ID utente non sia rintracciabile nuovamente dall’origine dal MVPD.   Questo ID è univoco e tipicamente persistente, ma non può essere condiviso con l&#39;MVPD per confrontare comportamenti di utilizzo specifici con quelli degli MVPD sul loro lato.   Non è firmato digitalmente, quindi non è inalterabile per la prevenzione delle frodi, ma è sufficiente per l&#39;analisi.  Questo modulo dell’ID utente viene fornito lato client su tutti gli eventi generati dall’autenticazione Adobe Primetime nel flusso AuthN/AuthZ.
* Token per contenuti multimediali brevi `sessionGUID` proprietà : è lo stesso dell&#39;ID utente tramite `sendTrackingData()`Tuttavia, questa viene firmata digitalmente per proteggere la sua integrità.  Ciò rende questo valore sufficientemente valido per il monitoraggio delle frodi dell’utilizzo simultaneo. Deve essere elaborato sul lato server dopo aver utilizzato la libreria di convalida e può essere analizzato per individuare i pattern di frode prima di rilasciare il flusso video al client.  Eseguire uno di questi compiti è compito del programmatore.
* `getMetadata() userID `proprietà - Questa proprietà consente ad Adobe di esporre l&#39;ID utente MVPD di origine effettiva al programmatore. Sarà crittografato con la chiave pubblica dal certificato che abbiamo dal programmatore, in modo che non sia esposto nel chiaro al cliente. Questo dà al programmatore l&#39;ID utente effettivo dall&#39;MVPD, quindi è qualcosa che può essere utilizzato per il collegamento dell&#39;account o le indagini di frode direttamente con l&#39;MVPD.

**In conclusione**

* L&#39;ID utente MVPD è un ID univoco persistente che è generalmente, anche se non garantito **generato dagli MVPD e passato ad Adobe in caso di autenticazione riuscita**. In genere è coerente in tutte le reti, con alcune eccezioni.
* L&#39;ID utente MVPD non contiene PII e NON è un numero di account. Non è necessario esporlo in forma criptata poiché abbiamo convalidato con tutti gli MVPD che non viene inviato alcun PII.


La modalità di utilizzo dell’ID utente dipende dal caso d’uso:

* Se necessario per il tracciamento/analisi, il posto più pratico è quello di ottenerlo da `sendTrackingData()`.
* Se è necessario sul lato server per il rilascio del flusso, la frode o i dati operativi, puoi ottenerlo da Media Token Validator.
* Se ti serve per il collegamento dell&#39;account e la frode più profonda, controlla con il tuo contatto Adobe per la disponibilità.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->