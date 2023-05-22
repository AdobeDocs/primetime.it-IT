---
title: Panoramica di MVPD
description: Panoramica di MVPD
exl-id: b918550b-96a8-4e80-af28-0a2f63a02396
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---

# Panoramica degli MVPD {#mvpd-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro}

Questa panoramica è destinata ai distributori di programmi video multicanale (MVPD). Per ulteriore documentazione, comprese le guide di Kick-Start e all’integrazione, consulta la sezione Informazioni correlate alla fine del presente documento.



TV Everywhere (TVE) è l&#39;ormai noto movimento del settore che consente agli abbonati a PayTV di accedere ai contenuti per i quali già pagano, su più dispositivi, sia dentro che fuori dalle loro case.  Per i fornitori di servizi di televisione a pagamento, TVE crea nuove opportunità, sia per preservare le relazioni con i clienti esistenti che per abilitarne di nuove. Ma insieme a queste opportunità ci sono delle sfide. Nel panorama TVE, i programmatori forniscono il contenuto, ma i MVPD conservano le informazioni del cliente per verificare che i potenziali visualizzatori siano abbonati validi.



Coordinare l&#39;autenticazione e l&#39;autorizzazione del visualizzatore con un programmatore può essere semplice, ma il coordinamento con decine o centinaia di programmatori diversi diventa sempre più complesso. Tuttavia, con Adobe® Pass, gli MVPD devono solo implementare un&#39;unica e semplice integrazione per accedere all&#39;intero ecosistema TVE, inclusi i programmatori come NBCUniversal Media, Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, Hulu e così via.  L’autenticazione Adobe Primetime fornisce un framework di integrazione che rende semplice e sicuro determinare la licenza dell’utente.



Ultima linea: l’autenticazione Adobe Primetime media in modo sicuro le transazioni di adesione tra Programmatori e MVPD, facilitando l’accesso degli utenti ai contenuti in abbonamento. In altre parole, l’autenticazione Adobe Primetime semplifica e velocizza l’accesso dei clienti giusti ai contenuti corretti.


Con l’autenticazione Adobe Primetime, gli MVPD ricevono:

Facile integrazione con i programmatori.  Connettività immediata da più proprietari di contenuti con un&#39;unica integrazione.

Migliore coinvolgimento dei clienti.  Supporta un’esperienza fluida e di marca, in quanto i clienti visualizzano i contenuti su più piattaforme e dispositivi.

Autenticazione sicura.  Assicurati che solo gli utenti e i dispositivi autorizzati possano accedere ai contenuti premium e (facoltativamente) limita il numero di dispositivi e flussi simultanei che possono connettersi per ogni account domestico.

## Domande frequenti {#faq}

Quanto è sicura l’autenticazione Adobe Primetime? La priorità numero uno dell’architettura di autenticazione di Adobe Primetime è garantire che solo i visualizzatori autorizzati siano autenticati e abbiano accesso ai contenuti premium. L’autenticazione Adobe Primetime associa strettamente l’accesso ai dispositivi di visualizzazione e può aiutare a limitare flussi, sessioni e/o dispositivi per una determinata famiglia.


È necessario specificare un Flash Player? L’autenticazione Adobe Primetime per TV Everywhere è indipendente dal lettore e dalla piattaforma, e si integra con qualsiasi applicazione di riproduzione, inclusi Silverlight e HTML5. Inoltre, l’autenticazione Adobe Primetime fornisce supporto nativo per dispositivi quali telefoni e tablet con iOS e Android.


Quali dispositivi sono supportati dall’autenticazione Adobe Primetime? L’autenticazione Adobe Primetime è supportata praticamente da qualsiasi dispositivo con il kit web HTML5 per le esperienze di visualizzazione nel browser. Inoltre, l’autenticazione Adobe Primetime continua a distribuire kit di sviluppo software nativi (SDK) per varie piattaforme specifiche per dispositivi, tra cui iOS, Android™, Xbox360 (obsoleto) e le applicazioni Adobe Air® (obsoleto). Più di recente, l’autenticazione Adobe Primetime ha messo a punto una soluzione senza client per i dispositivi che non possono eseguire il rendering delle pagine del browser (ad esempio, TV &quot;intelligenti&quot;, set-top box e console di gioco).  La possibilità di eseguire il rendering delle pagine del browser è un requisito per l’autenticazione degli utenti con MVPD.


L’autenticazione Adobe Primetime supporta gli standard emergenti per TV Everywhere? L’autenticazione di Adobe Primetime è conforme alle specifiche CableLabs OLCA (Online Content Access), che fornisce requisiti tecnici e architettura per la distribuzione di video a un cliente di Pay TV da origini online. Adobe ha partecipato al progetto congiunto di test di interoperabilità CableLabs nel giugno 2011 e ha superato il processo di test per un&#39;implementazione di Service Provider. L’autenticazione Adobe Primetime viene verificata (completa e testata) in base alle specifiche OLCA per l’autenticazione. Il componente di autorizzazione è stato completato, ma la verifica dei test attende attualmente il rilascio dell&#39;ambiente di test di CableLabs. Adobe è anche membro attivo dell&#39;OATC (Open Authentication Technical Consortium) e partecipa a diversi progetti di definizione delle specifiche dei sottocomitati come parte di tale organismo.



Che cos’è l’autenticazione? L&#39;autenticazione è il processo in cui un MVPD conferma che un determinato utente è un cliente noto.



Cos’è l’autorizzazione? L&#39;autorizzazione è il processo in cui un MVPD conferma che un utente autenticato dispone di un abbonamento valido a una determinata risorsa.



## Architettura {#architecture}

L’autenticazione Adobe Primetime è un servizio ospitato che consente una rapida integrazione back-end (server-to-server) basata sulle regole di business richieste sia dagli MVPD che dai programmatori. Ciò significa tempi di commercializzazione rapidi per tutte le parti, un ambiente più sicuro per prevenire le frodi e una migliore esperienza del cliente, con più contenuti TV disponibili per più persone su più piattaforme.


L’autenticazione Adobe Primetime viene offerta tramite il modello Software as a Service (SaaS) e consente comunicazioni più sicure tra utenti finali, MVPD e programmatori, al fine di convalidare l’adesione ai contenuti. I componenti principali del servizio includono:

Lato server: il server di autenticazione di Adobe Primetime in hosting. Si tratta di un application server che interagisce con la comunicazione back channel (server-to-server) con i sistemi di autenticazione degli MVPD.
Client Side: l&#39;Access Enabler lato client: l&#39;Access Enabler è un file di piccole dimensioni caricato nella pagina Web o nell&#39;applicazione di un programmatore. Fornisce API di adesione all’applicazione di visualizzazione dei contenuti del programmatore e comunica con il server di autenticazione di Adobe Primetime.
Servizi web senza client (per dispositivi non compatibili con il web): servizi web RESTful che forniscono API di adesione per dispositivi quali Smart TV, console per giochi e set-top box.

>[!NOTE]
>
>In qualità di MVPD, i servizi web devono essere in grado di riconoscere le richieste di autenticazione e autorizzazione dell’autenticazione Adobe Primetime e di rispondere con i dati richiesti nel formato previsto.

L’autenticazione Adobe Primetime consente di fornire ai clienti la gestione federata delle identità, nota anche come autenticazione e autorizzazione Single Sign-On (SSO). Con l’autenticazione Adobe Primetime, gli abbonati non dovranno effettuare di nuovo l’accesso dopo la prima autenticazione, fino a quando quest’ultima sarà consentita dall’MVPD. In genere, 30 giorni. A tal fine, l’autenticazione Adobe Primetime fornisce ai clienti un dominio comune per i token di autenticazione. Queste informazioni sullo stato di autenticazione sono disponibili per tutti i siti partecipanti che sono integrati con un dato MVPD.


Attualmente, la maggior parte delle integrazioni di autenticazione Adobe Primetime con MVPD utilizza il protocollo SAML, uno degli standard di autenticazione primari. L’autenticazione Adobe Primetime funge da provider di servizi proxy nell’architettura SAML e mantiene la risposta di autenticazione SAML come token sicuro nel dominio comune di Adobe. L’autenticazione di Adobe Primetime è conforme a SAML 2.0. Tuttavia, anche se a questo punto l’autenticazione Adobe Primetime viene generalmente utilizzata con le soluzioni SAML SSO, l’architettura di autenticazione Adobe Primetime non è associata ad alcun protocollo specifico. Pertanto, è possibile aggiungere nel tempo il supporto per nuovi protocolli, ad esempio quelli basati su OAuth 2.0 o su protocolli personalizzati.


Adobe collabora con un team tecnico di MVPD per configurare l’autenticazione di Adobe Primetime in modo da soddisfare le esigenze di eventuali integrazioni esistenti. L&#39;integrazione è gratuita per gli MVPD, presumendo un&#39;integrazione &quot;standard&quot; e requisiti minimi di supporto (documentazione e supporto e-mail di base). Se un MVPD richiede un supporto significativo o una tempistica aumentata, è possibile che venga addebitata una tariffa di supporto o che il fornitore desideri collaborare con una terza parte che ha familiarità con la nostra soluzione, come Synacor.


L’autenticazione Adobe Primetime supporta anche la gestione efficiente della logica di business MVPD, come segue:

Per la logica di business che è indipendente e può essere applicata dal MVPD quando viene ricevuta una richiesta di autorizzazione, Adobe fornisce i dati necessari necessari per supportare l&#39;applicazione della logica di business quando il MVPD riceve una richiesta di autorizzazione. Questi dati possono includere, tra l’altro, l’ID dispositivo univoco dell’utente che effettua la richiesta e l’indirizzo IP del dispositivo.

Per la logica di business che richiede l’intervento dell’utente e/o la gestione specifica da parte della soluzione Adobe, Adobe può mantenere alcune proprietà personalizzate per ogni MVPD. Queste configurazioni/policy specifiche per MVPD includono l’abilitazione di flussi di lavoro predefiniti che possono essere avviati in punti specifici del flusso di lavoro di primo livello. Per informazioni dettagliate sul supporto delle proprietà personalizzate, contatta il rappresentante del tuo Adobe.

Il diagramma seguente illustra la relazione tra MVPD e il programmatore con questi componenti di autenticazione Adobe Primetime:

![](assets/high-level-architecture-nflows.png)

*Figura: Architettura e flussi di alto livello*

## Componenti di autenticazione di Adobe Primetime {#components}

Di seguito viene fornita una panoramica di alcuni dei componenti principali dell’ecosistema di autenticazione Adobe Primetime. Tra questi:

* [Servizi Web Access Enabler/senza client](#ae)
* [Server back-end ospitato da Adobe](#backend)
* [Token](#tokens)

### Access Enabler / Servizi Web senza client {#ae}

L’Access Enabler facilita tutte le interazioni di autenticazione e autorizzazione con l’utente ed è eseguito localmente sul suo sistema. È l’Access Enabler che gestisce i flussi di lavoro effettivi per adesione con MVPD, mentre il Programmatore mantiene la responsabilità per la pagina web di livello superiore o l’applicazione del lettore.

I servizi web senza client vengono forniti dall’autenticazione di Adobe Primetime per i dispositivi che non possono eseguire il rendering di pagine web.  Per questi dispositivi, il processo di adesione viene avviato e il contenuto visualizzato sul dispositivo intelligente, mentre l’autenticazione con un MVPD avviene su un dispositivo compatibile con il web (PC, smartphone e tablet).

L&#39;Access Enabler:

* Avvia flussi di lavoro di autenticazione e autorizzazione specifici per MVPD.
* Memorizza nella cache le risposte di autorizzazione riuscite per risorsa/canale del programmatore per ridurre al minimo il traffico di richieste non necessario.
* Può essere configurato per flussi di lavoro predefiniti specifici per ogni MVPD, ad esempio la registrazione esplicita del dispositivo.
* È disponibile nei seguenti formati:
   * Un file SWF che il runtime di Flash Player può eseguire
   * Un file JS eseguito direttamente dal browser
   * Un Access Enabler nativo per varie piattaforme, tra cui iOS, Android e Xbox.

### Server back-end ospitato da Adobe {#backend}

Il server back-end di autenticazione di Adobe Primetime, ospitato da Adobe:

* Esegue il provisioning dei flussi di lavoro di autenticazione e autorizzazione con gli MVPD che richiedono la comunicazione server-to-server tra l’autenticazione di Adobe Primetime e l’operatore.
* Mantiene la configurazione per i siti e le applicazioni del programmatore.
* Ospita i file dei componenti scaricabili di Access Enabler.
* Genera token di autenticazione e autorizzazione.

### Token {#tokens}

La soluzione Adobe Primetime per l’autenticazione è incentrata sulla generazione di parti specifiche di dati ottenuti al completamento dei flussi di lavoro di autenticazione/autorizzazione. Questi dati sono denominati token. Hanno una durata limitata e sono archiviati in modo sicuro in posizioni dipendenti dalla piattaforma. Alla scadenza, i token devono essere ririlasciati riavviando i flussi di lavoro di autenticazione e/o autorizzazione.

Esistono tre tipi di token rilasciati durante i flussi di lavoro di autenticazione/autorizzazione. Due sono &quot;di lunga durata&quot; e forniscono continuità nell’esperienza di visualizzazione dell’utente. Il terzo, un token di breve durata, fornisce supporto per le best practice del settore per ridurre le frodi attraverso la copia di flusso. I valori time-to-live (&quot;TTL&quot;) per i token sono impostati in base agli accordi tra MVPD e Programmatori. Puoi scegliere un valore TTL che soddisfi al meglio le esigenze della tua azienda e dei tuoi clienti.

**Token di autenticazione di lunga durata**. L’autenticazione ha esito positivo quando un cliente utilizza l’autenticazione Adobe Primetime per accedere correttamente al proprio account MVPD. L’autenticazione Adobe Primetime genera quindi un token di autenticazione di lunga durata (&quot;authN&quot;) associato al dispositivo richiedente e (a seconda dell’MVPD) un identificatore univoco globale (&quot;GUID&quot;) che identifica l’utente in modo anonimo.

**Il token di autorizzazione a vita lunga**. In caso di esito positivo dell’autorizzazione, l’autenticazione Adobe Primetime crea un token di autorizzazione di lunga durata (&quot;authZ&quot;). Questo token non è portatile, in quanto è associato al dispositivo richiedente e a una risorsa protetta specifica (ad esempio un canale, una serie o un episodio). L’Access Enabler utilizza il token authZ di lunga durata per creare i token multimediali di breve durata utilizzati per l’accesso effettivo alla visualizzazione.

**Il token multimediale di breve durata**. Una volta che l’utente è autorizzato, l’autenticazione Adobe Primetime genera un token authZ e lo utilizza per generare un token multimediale monouso di breve durata firmato da Adobe e crittografato per evitare manomissioni durante lo scambio. Poiché il token di breve durata è esposto al sito di incorporamento tramite l’API Access Enabler o i servizi Web Clientless, prima di fornire l’accesso alla risorsa protetta, il server multimediale del programmatore deve utilizzare un componente di autenticazione Adobe Primetime, Media Token Verifier, per convalidare il token.

## Ciclo di vita dell&#39;integrazione MVPD {#lifecycle}

L’illustrazione seguente mostra il ciclo di vita dell’integrazione tra l’autenticazione Adobe Primetime e un MVPD.

![](assets/mvpd-int-lifecycle.png)

*Figura: ciclo di vita dell&#39;integrazione MVPD*

## Diagramma di flusso diritto {#chart}

Il seguente diagramma di flusso illustra il processo complessivo di conferma dell’adesione tramite l’autenticazione Adobe Primetime:

![](assets/authn-authz-entitlmnt-flow.png)

*Figura: Processo di conferma dell’adesione tramite l’autenticazione Adobe Primetime*

## Passaggi di autenticazione {#authn-steps}

I passaggi seguenti presentano un esempio del flusso di autenticazione di Adobe Primetime.  Questa è la parte del processo di adesione in cui un programmatore determina se l&#39;utente è un cliente valido di un MVPD.  In questo caso, l’utente è un abbonato valido a un MVPD.  L’utente sta tentando di visualizzare il contenuto protetto utilizzando un’applicazione di Flash del programmatore:

1. L’utente passa alla pagina web del programmatore, che carica l’applicazione di Flash del programmatore e i componenti Adobe Primetime authentication Access Enabler sul computer dell’utente. L&#39;applicazione di Flash utilizza Access Enabler per impostare l&#39;identificazione del programmatore con l&#39;autenticazione Adobe Primetime e l&#39;autenticazione Adobe Primetime prepara l&#39;Access Enabler con i dati di configurazione e stato per quel programmatore (il &quot;richiedente&quot;). L’Access Enabler deve ricevere questi dati dal server prima di eseguire qualsiasi altra chiamata API.  Nota tecnica: il programmatore imposta la propria identità con l’opzione di abilitazione all’accesso `setRequestor()` metodo; per ulteriori informazioni, vedere [Guida all’integrazione dei programmatori](/help/authentication/programmer-integration-guide-overview.md).
1. Quando l&#39;utente cerca di visualizzare il contenuto protetto del programmatore, l&#39;applicazione del programmatore presenta all&#39;utente un elenco di MVPD, da cui l&#39;utente seleziona un provider.
1. L’utente viene reindirizzato a un server di autenticazione di Adobe Primetime, in cui viene creata una richiesta SAML crittografata per l’MVPD selezionato dall’utente. Questa richiesta viene inviata come richiesta di autenticazione per conto del programmatore a MVPD. A seconda del sistema dell&#39;MVPD, il browser dell&#39;utente viene quindi reindirizzato al sito dell&#39;MVPD per effettuare l&#39;accesso, oppure viene creato un iFrame di accesso nell&#39;app del programmatore.
1. In entrambi i casi (redirect o iFrame), MVPD accetta la richiesta e visualizza la relativa pagina di accesso.
1. L&#39;utente accede con MVPD, quest&#39;ultimo convalida lo stato dell&#39;utente come cliente pagante e quindi crea la propria sessione HTTP.
1. Quando l’utente viene convalidato, MVPD crea una risposta (SAML e crittografata) che viene inviata nuovamente all’autenticazione di Adobe Primetime.
1. L’autenticazione Adobe Primetime riceve la risposta MVPD, rileva che è aperta una sessione HTTP di autenticazione Adobe Primetime e convalida la [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) dal MVPD e reindirizza al sito del programmatore.
1. Il sito del programmatore viene ricaricato, l&#39;Access Enabler viene ricaricato e il programmatore chiama nuovamente setRequestor().  La seconda chiamata a setRequestor() è necessaria perché la configurazione corrente è stata modificata. È ora presente un flag che informa Access Enabler che un token AuthN è in attesa di essere generato sul server.
1. Access Enabler rileva un’autenticazione in sospeso e richiede il token dal server di autenticazione di Adobe Primetime. Il token viene recuperato dal server richiamando le funzionalità DRM del Flash Player.
1. Il token AuthN viene memorizzato nella cache LSO del Flash Player del programmatore; l’autenticazione è ora completa e la sessione viene eliminata sul server di autenticazione di Adobe Primetime.

## Passaggi di autorizzazione {#authz-steps}

I seguenti passaggi proseguono dalla sezione precedente ([Passaggi di autenticazione](#authn-steps)):

1. Quando l’utente tenta di accedere al contenuto protetto del Programmatore, l’applicazione del Programmatore verifica innanzitutto la presenza di un token AuthN sul computer o sul dispositivo locale dell’utente.  Se tale token non è presente, il token [Passaggi di autenticazione](#authn-steps) sono seguite le indicazioni precedenti.  Se il token AuthN è presente, il flusso di autorizzazione procede con l’applicazione del programmatore che avvia una chiamata all’Access Enabler con una richiesta per ottenere i diritti di visualizzazione dell’utente per un elemento specifico di contenuto protetto.
1. L’elemento specifico di contenuto protetto è rappresentato da un &quot;identificatore di risorsa&quot;.  Potrebbe trattarsi di una stringa semplice o di una struttura più complessa, ma in ogni caso la natura dell’identificatore della risorsa viene concordata in anticipo tra il Programmatore e l’MVPD.  L&#39;applicazione del programmatore passa l&#39;identificatore della risorsa all&#39;Access Enabler.  Access Enabler verifica la presenza di un token AuthZ sul computer o sul dispositivo locale dell&#39;utente.  Se il token AuthZ non è presente, Access Enabler trasmette la richiesta al server di autenticazione Adobe Primetime back-end.
1. Il server di autenticazione di Adobe Primetime comunica con l’endpoint di autorizzazione MVPDs utilizzando protocolli standardizzati.  Se la risposta dell’MVPD indica che l’utente ha il diritto di visualizzare il contenuto protetto, il server di autenticazione di Adobe Primetime crea un token AuthZ e lo trasmette nuovamente all’Access Enabler, che memorizza il token AuthZ sul computer dell’utente.
1. Con un token AuthZ memorizzato sul computer o sul dispositivo dell’utente, l’applicazione del programmatore chiama l’Access Enabler per ottenere un token multimediale dal server di autenticazione di Adobe Primetime e fornisce tale token all’applicazione del programmatore.
1. Infine, l’applicazione del programmatore utilizza il componente Media Token Verifier per confermare che l’utente giusto sta visualizzando il contenuto corretto e, con il Media Token attivo, può visualizzare il contenuto protetto.

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
