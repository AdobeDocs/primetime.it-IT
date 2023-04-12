---
title: Panoramica per gli MVPD
description: Panoramica per gli MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# Panoramica degli MVPD {#mvpd-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#intro}

Questa panoramica è destinata ai distributori MVPD (Multi-Channel Video Programming Distributor). Per ulteriore documentazione, incluse le guide di Kickstart e Integrazione, consulta la sezione Informazioni correlate alla fine di questo documento.



TV Everywhere (TVE) è l&#39;ormai noto movimento industriale che consente agli abbonati a Pay TV di accedere ai contenuti che già pagano, attraverso più dispositivi, sia all&#39;interno che all&#39;esterno delle loro case.  Per i fornitori di Pay TV, TVE crea nuove opportunità, sia per mantenere le relazioni con i clienti esistenti che per abilitarne di nuove. Ma insieme a queste opportunità ci sono delle sfide. Nel panorama TVE, i programmatori forniscono il contenuto, ma gli MVPD contengono le informazioni del cliente per verificare che i potenziali visualizzatori siano abbonati validi.



Coordinare l&#39;autenticazione e l&#39;autorizzazione dei visualizzatori con un programmatore può essere semplice, ma il coordinamento con decine o centinaia di programmatori diversi diventa sempre più complesso. Tuttavia, con Adobe® Pass, gli MVPD devono implementare un&#39;unica integrazione semplice per accedere all&#39;intero ecosistema TVE, inclusi programmatori come NBCUniversal Media, Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, Hulu e così via.  L’autenticazione Adobe Primetime fornisce un framework di integrazione che rende semplice e sicuro determinare l’adesione degli utenti.



Linea inferiore: L’autenticazione Adobe Primetime consente di mediare in modo sicuro le transazioni di adesione tra programmatori e MVPD, facilitando l’accesso del visualizzatore al contenuto dell’abbonamento. In altre parole, l’autenticazione Adobe Primetime consente ai clienti giusti di accedere facilmente e rapidamente ai contenuti giusti.


Con l’autenticazione Adobe Primetime, gli MVPD ricevono:

Facile integrazione con i programmatori.  Offri connettività immediata a più proprietari di contenuti con un’unica integrazione.

Maggiore coinvolgimento dei clienti.  Supporta un’esperienza fluida e con marchio in quanto i clienti visualizzano i contenuti su più piattaforme e dispositivi.

Autenticazione sicura.  Assicurati che solo gli utenti e i dispositivi autorizzati abbiano accesso ai contenuti premium e (facoltativamente) limiti il numero di dispositivi e flussi simultanei che possono connettersi per account domestico.

## Domande frequenti {#faq}

Quanto è sicura l’autenticazione Adobe Primetime? La priorità numero uno dell’architettura di autenticazione di Adobe Primetime è garantire che solo i visualizzatori autorizzati siano autenticati e abbiano accesso ai contenuti premium. L’autenticazione Adobe Primetime lega strettamente l’accesso ai dispositivi di visualizzazione e può contribuire a limitare flussi, sessioni e/o dispositivi per una determinata famiglia.


È richiesto il Flash Player? Autenticazione Adobe Primetime per TV Everywhere è indipendente dal lettore e dalla piattaforma, che si integra con qualsiasi applicazione di riproduzione, inclusi Silverlight e HTML5. Inoltre, l’autenticazione Adobe Primetime fornisce supporto nativo per dispositivi come telefoni e tablet con iOS e Android.


Quali dispositivi supporta l’autenticazione Adobe Primetime? L’autenticazione Adobe Primetime è supportata praticamente da qualsiasi dispositivo con il kit web HTML5 per le esperienze di visualizzazione nel browser. Inoltre, l’autenticazione Adobe Primetime continua a distribuire kit di sviluppo software nativi (SDK) per diverse piattaforme specifiche per dispositivi, tra cui iOS, Android™, Xbox360 (obsoleto) e le applicazioni Adobe Air® (obsoleto). Più di recente, l’autenticazione Adobe Primetime ha implementato una soluzione Clientless per dispositivi che non possono eseguire il rendering delle pagine del browser (ad esempio, TV &quot;intelligenti&quot;, set-top box e console di gioco).  La capacità di eseguire il rendering delle pagine del browser è un requisito per l’autenticazione degli utenti con gli MVPD.


L&#39;autenticazione Adobe Primetime supporta gli standard emergenti per TV Everywhere? L’autenticazione Adobe Primetime è conforme alla specifica CableLabs OLCA (Online Content Access), che fornisce requisiti tecnici e architettura per la distribuzione di video a un cliente Pay TV da fonti online. L&#39;Adobe ha partecipato al progetto congiunto di test interopt CableLabs nel giugno 2011 e ha superato il processo di test per un&#39;implementazione Service Provider. L’autenticazione Adobe Primetime viene verificata (completa e verificata) in base alle specifiche OLCA per l’autenticazione. Il componente di autorizzazione è completato, ma la verifica del test attende attualmente il rilascio dell&#39;ambiente di test CableLabs. L&#39;Adobe è anche un membro attivo dell&#39;OATC (Open Authentication Technical Consortium) e partecipa a diversi progetti di elaborazione delle specifiche dei sottocomitati nell&#39;ambito di tale organismo.



Cos’è l’autenticazione? L&#39;autenticazione è il processo in cui un MVPD conferma che un dato utente è un cliente noto.



Che cos’è l’autorizzazione? L’autorizzazione è il processo in cui un MVPD conferma che un utente autenticato ha una sottoscrizione valida a una determinata risorsa.



## Architettura {#architecture}

Adobe Primetime Authentication è un servizio in hosting che consente l&#39;integrazione rapida back-end (server to server) in base alle regole aziendali richieste da MVPD e programmatori. Questo significa un rapido time-to-market per tutte le parti, un ambiente più sicuro per prevenire le frodi e una customer experience superiore, con più contenuti TV disponibili per più persone su più piattaforme.


L’autenticazione Adobe Primetime viene offerta tramite il modello Software as a Service (SaaS) e consente una comunicazione più sicura tra utenti finali, MVPD e programmatori, al fine di convalidare l’adesione al contenuto. I componenti core del servizio includono:

Lato server: server di autenticazione Adobe Primetime in hosting. Si tratta di un server applicativo che effettua una comunicazione back channel (server-to-server) con i sistemi di autenticazione degli MVPD.
Lato client: Access Enabler lato client: Access Enabler è un piccolo file caricato nella pagina web o nell&#39;applicazione di riproduzione di un programmatore. Fornisce API di adesione all&#39;applicazione di visualizzazione del contenuto del programmatore e comunica con Adobe Primetime Authentication Server.
Servizi web senza client (per dispositivi non adatti al web) - Servizi web RESTful che forniscono API di adesione per dispositivi quali Smart TV, console giochi e set-top box.

>[!NOTE]
>
>In qualità di MVPD, i servizi web devono essere in grado di riconoscere le richieste di autenticazione e autorizzazione dall’autenticazione Adobe Primetime e di rispondere con i dati richiesti nel formato previsto.

L’autenticazione Adobe Primetime ti consente di fornire ai clienti una gestione federata dell’identità, nota anche come autenticazione e autorizzazione single sign-on (SSO). Con l’autenticazione Adobe Primetime, non è necessario che gli abbonati effettuino di nuovo l’accesso dopo la loro prima autenticazione, purché tale autenticazione sia consentita dall’MVPD. In genere, 30 giorni. A tal fine, Adobe Primetime Authentication fornisce un dominio comune per i token di autenticazione per i nostri clienti. Queste informazioni sullo stato di autenticazione sono disponibili per tutti i siti partecipanti che sono integrati con un MVPD specifico.


Attualmente, la maggior parte delle integrazioni di autenticazione Adobe Primetime con MVPD utilizza il protocollo SAML, uno degli standard di autenticazione principali. L’autenticazione Adobe Primetime agisce come proxy Service Provider nell’architettura SAML e persiste la risposta di autenticazione SAML come token sicuro nel dominio comune di Adobe. L’autenticazione Adobe Primetime è conforme a SAML 2.0. Tuttavia, mentre a questo punto l&#39;autenticazione Adobe Primetime viene generalmente utilizzata con le soluzioni SSO SAML, l&#39;architettura di autenticazione Adobe Primetime non è vincolata ad alcun protocollo specifico. Pertanto, è possibile aggiungere nel tempo il supporto per i nuovi protocolli, ad esempio quelli basati su OAuth 2.0 o su protocolli personalizzati.


Adobe collabora con il team tecnico di un MVPD per configurare l’autenticazione Adobe Primetime in modo da soddisfare le esigenze di eventuali integrazioni esistenti. L&#39;integrazione è gratuita per gli MVPD, supponendo un&#39;integrazione &quot;standard&quot; e requisiti minimi di supporto (documentazione e supporto e-mail di base). Se un MVPD richiede un supporto significativo o una tempistica avanzata, può essere addebitata una tariffa di supporto, o il fornitore può voler lavorare con una terza parte che ha familiarità con la nostra soluzione, come Synacor.


L’autenticazione Adobe Primetime supporta anche la gestione efficiente della logica di business MVPD, come segue:

Per la logica di business che è indipendente e può essere applicata dall&#39;MVPD quando viene ricevuta una richiesta di autorizzazione, Adobe fornisce i dati necessari per supportare l&#39;applicazione della logica di business quando l&#39;MVPD riceve una richiesta di autorizzazione. Questi dati possono includere, ma non sono limitati a, l&#39;ID dispositivo univoco per l&#39;utente che effettua la richiesta e l&#39;indirizzo IP del dispositivo.

Per la logica di business che richiede l’intervento dell’utente e/o la gestione specifica da parte della soluzione Adobe, Adobe può mantenere alcune proprietà personalizzate per ogni MVPD. Queste configurazioni/criteri specifici per MVPD includono l’abilitazione di flussi di lavoro predefiniti che possono essere avviati in punti specifici del flusso di lavoro di livello principale. Per informazioni sul supporto delle proprietà personalizzate, contatta il tuo rappresentante di Adobe.

Il diagramma seguente illustra il rapporto tra MVPD e programmatore e questi componenti di autenticazione Adobe Primetime:

![](assets/high-level-architecture-nflows.png)

*Figura: Architettura e flussi di alto livello*

## Componenti di autenticazione di Adobe Primetime {#components}

Di seguito viene fornita una panoramica di alcuni dei componenti principali dell’ecosistema di autenticazione Adobe Primetime. Tra questi figurano:

* [Access Enabler / Client Web Services](#ae)
* [Server di back-end ospitato da Adobe](#backend)
* [Token](#tokens)

### Accesso a Enabler / Servizi Web Clientless {#ae}

Access Enabler facilita tutte le interazioni di autenticazione e autorizzazione con l&#39;utente ed esegue localmente sul proprio sistema. È l&#39;Access Enabler che gestisce i flussi di lavoro di adesione effettivi con l&#39;MVPD, mentre il programmatore mantiene la responsabilità per la pagina web o l&#39;applicazione di riproduzione di livello superiore.

I servizi web senza client sono forniti dall’autenticazione Adobe Primetime per dispositivi che non possono eseguire il rendering di pagine web.  Per questi dispositivi, il processo di adesione viene avviato e il contenuto viene visualizzato sul dispositivo intelligente, mentre l&#39;autenticazione con un MVPD avviene su un dispositivo compatibile con il web (PC, smartphone e tablet).

Access Enabler:

* Avvia flussi di lavoro di autenticazione e autorizzazione specifici per MVPD.
* Memorizza in cache le risposte di autorizzazione corrette per risorsa/canale programmatore per ridurre al minimo il traffico di richieste non necessarie.
* Può essere configurato per flussi di lavoro predefiniti specifici per ogni MVPD, ad esempio per la registrazione esplicita del dispositivo.
* È disponibile nei seguenti moduli:
   * File SWF eseguibile dal runtime di Flash Player
   * Un file JS eseguito direttamente dal browser
   * Un enabler nativo per diverse piattaforme, tra cui iOS, Android e Xbox.

### Server back-end ospitato da Adobe {#backend}

Server back-end di autenticazione Adobe Primetime, ospitato da Adobe:

* Assegna i flussi di lavoro di autenticazione e autorizzazione con gli MVPD che richiedono una comunicazione server-to-server tra l’autenticazione Adobe Primetime e l’operatore.
* Mantiene la configurazione dei siti e delle applicazioni Programmer.
* Ospita i file dei componenti di Access Enabler scaricabili.
* Genera token di autenticazione e autorizzazione.

### Token {#tokens}

La soluzione di adesione all&#39;autenticazione di Adobe Primetime si basa sulla generazione di parti di dati specifiche ottenute al completamento dei flussi di lavoro di autenticazione/autorizzazione. Questi dati sono chiamati token. Hanno una durata di vita limitata e sono memorizzati in modo sicuro in posizioni dipendenti dalla piattaforma. Alla scadenza, i token devono essere riemessi tramite il riavvio dei flussi di lavoro di autenticazione e/o autorizzazione.

Durante i flussi di lavoro di autenticazione/autorizzazione vengono rilasciati tre tipi di token. Due sono &quot;longevi&quot;, che forniscono continuità nell&#39;esperienza visiva dell&#39;utente. Il terzo, un token di breve durata, fornisce supporto per le best practice del settore per mitigare le frodi attraverso la rimozione dei flussi. I valori time-to-live (&quot;TTL&quot;) per i token sono impostati sulla base di accordi tra MVPD e programmatori. Si decide il valore TTL più adatto alla propria azienda e ai propri clienti.

**Token di autenticazione longevo**. L&#39;autenticazione si verifica quando un cliente utilizza l&#39;autenticazione Adobe Primetime per accedere correttamente al proprio account MVPD. L’autenticazione Adobe Primetime produce quindi un token di autenticazione a lungo termine (&quot;authN&quot;) associato al dispositivo richiedente e (a seconda dell’MVPD) un identificatore univoco globale (&quot;GUID&quot;) che identifica in modo anonimo l’utente.

**Il token di autorizzazione a lungo termine**. Una volta ottenuta l’autorizzazione, l’autenticazione Adobe Primetime crea un token di autorizzazione a lungo termine (&quot;authZ&quot;). Questo token non è portatile, in quanto è legato al dispositivo richiedente e a una risorsa protetta specifica (ad esempio un canale, una serie o un episodio). Access Enabler utilizza il token authZ a lunga vita per creare i token multimediali di breve durata utilizzati per l&#39;accesso effettivo alla visualizzazione.

**Il token multimediale di breve durata**. Una volta che l’utente è autorizzato, l’autenticazione Adobe Primetime genera un token authZ e utilizza tale token per generare un token multimediale di breve durata a uso singolo, firmato per Adobe e crittografato per evitare manomissioni durante lo scambio. Poiché il token di breve durata è esposto al sito di incorporamento tramite l’API di Access Enabler o i servizi web Clientless, prima di fornire l’accesso alla risorsa protetta, il server multimediale del programmatore deve utilizzare un componente di autenticazione Adobe Primetime, il Verificatore di token multimediali, per convalidare il token.

## Ciclo di vita dell&#39;integrazione MVPD {#lifecycle}

La figura seguente illustra il ciclo di vita dell’integrazione tra l’autenticazione Adobe Primetime e un MVPD.

![](assets/mvpd-int-lifecycle.png)

*Figura: Ciclo di vita dell&#39;integrazione MVPD*

## Diagramma di flusso di adesione {#chart}

Il seguente diagramma di flusso presenta il processo complessivo di conferma dell’adesione tramite l’autenticazione Adobe Primetime:

![](assets/authn-authz-entitlmnt-flow.png)

*Figura: Processo di conferma dell’adesione tramite autenticazione Adobe Primetime*

## Passaggi di autenticazione {#authn-steps}

I passaggi seguenti presentano un esempio del flusso di autenticazione dell’autenticazione di Adobe Primetime.  Questa è la parte del processo di adesione in cui un programmatore determina se l&#39;utente è un cliente valido di un MVPD.  In questo scenario, l&#39;utente è un abbonato valido a un MVPD.  L&#39;utente sta tentando di visualizzare il contenuto protetto utilizzando un&#39;applicazione di Flash del programmatore:

1. L&#39;utente passa alla pagina Web del programmatore, che carica l&#39;applicazione del Flash del programmatore e i componenti di Adobe Primetime Authentication Access Enabler sul computer dell&#39;utente. L&#39;applicazione di Flash utilizza Access Enabler per impostare l&#39;identificazione del programmatore con l&#39;autenticazione Adobe Primetime, e l&#39;autenticazione Adobe Primetime fornisce ad Access Enabler i dati di configurazione e stato per quel programmatore (il &quot;richiedente&quot;). Access Enabler deve ricevere questi dati dal server prima di eseguire qualsiasi altra chiamata API.  Nota tecnica: il programmatore imposta la propria identità con Access Enabler `setRequestor()` metodo; per ulteriori informazioni, consulta la [Guida all&#39;integrazione dei programmatori](/help/authentication/programmer-integration-guide-overview.md).
1. Quando l&#39;utente tenta di visualizzare il contenuto protetto del programmatore, l&#39;applicazione del programmatore presenta all&#39;utente un elenco di MVPD, da cui l&#39;utente seleziona un provider.
1. L’utente viene reindirizzato a un server di autenticazione Adobe Primetime, in cui viene creata una richiesta SAML crittografata per l’MVPD selezionato dall’utente. Questa richiesta viene inviata come richiesta di autenticazione per conto del programmatore al MVPD. A seconda del sistema MVPD, il browser dell&#39;utente viene quindi reindirizzato al sito MVPD per l&#39;accesso, oppure viene creato un iFrame di accesso nell&#39;app del programmatore.
1. In entrambi i casi (reindirizzamento o iFrame), l&#39;MVPD accetta la richiesta e visualizza la pagina di login.
1. L&#39;utente accede con l&#39;MVPD, l&#39;MVPD convalida lo stato dell&#39;utente come cliente pagante, e poi l&#39;MVPD crea la propria sessione HTTP.
1. Quando l&#39;utente viene convalidato, l&#39;MVPD crea una risposta (SAML e crittografato) che l&#39;MVPD invia nuovamente all&#39;autenticazione Adobe Primetime.
1. L&#39;autenticazione Adobe Primetime riceve la risposta MVPD, vede che c&#39;è una sessione HTTP di autenticazione Adobe Primetime aperta, convalida il [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) risposta dall&#39;MVPD e reindirizzerà al sito del programmatore.
1. Il sito del programmatore viene ricaricato, Access Enabler viene ricaricato e il programmatore richiama di nuovo setRequestor() .  La seconda chiamata a setRequestor() è necessaria perché la configurazione corrente è cambiata. È ora presente un flag che informa l&#39;utente che un token AuthN è in attesa di essere generato sul server.
1. Access Enabler rileva che è in sospeso l&#39;autenticazione e richiede il token dal server di autenticazione Adobe Primetime. Il token viene recuperato dal server richiamando le funzionalità DRM del Flash Player.
1. Il token AuthN è memorizzato nella cache LSO di Flash Player del programmatore; l’autenticazione è ora completa e la sessione viene eliminata sul server di autenticazione Adobe Primetime.

## Passaggi di autorizzazione {#authz-steps}

I seguenti passaggi continuano dalla sezione precedente ([Passaggi di autenticazione](#authn-steps)):

1. Quando l&#39;utente tenta di accedere al contenuto protetto del programmatore, l&#39;applicazione del programmatore controlla prima un token AuthN sul computer o sul dispositivo locale dell&#39;utente.  Se il token non è presente, il [Passaggi di autenticazione](#authn-steps) sono seguite le indicazioni di cui sopra.  Se il token AuthN è presente, il flusso di autorizzazione procede con l&#39;applicazione del programmatore che avvia una chiamata a Access Enabler con una richiesta per ottenere i diritti di visualizzazione dell&#39;utente per un elemento specifico di contenuto protetto.
1. L’elemento specifico del contenuto protetto è rappresentato da un &quot;identificatore di risorsa&quot;.  Può trattarsi di una stringa semplice o di una struttura più complessa, ma in ogni caso la natura dell&#39;identificativo della risorsa è concordata in anticipo tra il programmatore e l&#39;MVPD.  L&#39;applicazione del programmatore passa l&#39;identificatore della risorsa a Access Enabler.  Access Enabler controlla la presenza di un token AuthZ nel computer o nel dispositivo locale dell&#39;utente.  Se il token AuthZ non è presente, Access Enabler trasmette la richiesta al server di autenticazione Adobe Primetime back-end.
1. Il server di autenticazione Adobe Primetime comunica con l’endpoint di autorizzazione MVPD utilizzando protocolli standardizzati.  Se la risposta dell&#39;MVPD indica che l&#39;utente ha il diritto di visualizzare il contenuto protetto, il server di autenticazione Adobe Primetime crea un token AuthZ e lo ritrasmette all&#39;Access Enabler, che memorizza il token AuthZ sul computer dell&#39;utente.
1. Con un token AuthZ memorizzato sul computer o sul dispositivo dell&#39;utente, l&#39;applicazione del programmatore chiama Access Enabler per ottenere un token multimediale dal server di autenticazione Adobe Primetime e fornisce tale token all&#39;applicazione del programmatore.
1. Infine, l’applicazione del programmatore utilizza il componente Media Token Verifier per confermare che l’utente corretto sta visualizzando il contenuto corretto e con il token multimediale attivo, l’utente può visualizzare il contenuto protetto.

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
