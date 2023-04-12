---
title: Guida di riferimento API REST (server-to-server)
description: Rest del server di cookie API sul server.
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---


# Guida di riferimento API REST (server-to-server) {#rest-api-cookbook-server-to-server}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica {#overview}

Lo scopo di questo documento è quello di fornire informazioni sulle best practice per l’implementazione dell’autenticazione Adobe Primetime tramite le architetture server-to-server.  Fornisce requisiti di base, implementazione dettagliata del flusso e considerazioni generali per gli ambienti di produzione e il funzionamento.

 

## Componenti {#components}

In una soluzione Server-to-Server funzionante sono coinvolti i seguenti componenti:

 
| Tipo | Componente | Descrizione | | — | — | — | | Dispositivo di streaming | App in streaming | L&#39;applicazione Programmer che risiede sul dispositivo di streaming dell&#39;utente e riproduce il video autenticato. | | | \[Optional\] Modulo AuthN | se il dispositivo di streaming dispone di un agente utente (ad es. browser Web), il modulo AuthN è responsabile dell&#39;autenticazione dell&#39;utente nell&#39;IdP MVPD. | | \[Facoltativo\] Dispositivo AuthN | App AuthN | se il dispositivo di streaming non dispone di un agente utente (ad esempio il browser Web), l&#39;applicazione AuthN è un&#39;applicazione Web Programmer a cui si accede dal dispositivo di un utente separato utilizzando un browser web. | | Infrastruttura programmatica | Servizio programmatore | Servizio che collega il dispositivo di streaming a Adobe Pass Service per ottenere le decisioni relative all’autenticazione e all’autorizzazione. | | Infrastruttura Adobe | Servizio Adobe Pass | Un servizio che si integra con MVPD IdP e AuthZ Service e fornisce decisioni di autenticazione e autorizzazione. | | Infrastruttura MVPD | IdP MVPD | Un endpoint MVPD che fornisce un servizio di autenticazione basato sulle credenziali per convalidare l’identità dell’utente. | | | Servizio MVPD AuthZ | Un endpoint MVPD che fornisce decisioni di autorizzazione in base alle sottoscrizioni dell&#39;utente, ai controlli genitori, ecc. |


I termini aggiuntivi utilizzati nel flusso sono definiti nella variabile
[Glossario](/help/authentication/glossary.md).

## Flussi {#flows}

### Registrazione client dinamica (DCR)


Adobe Pass utilizza il DCR per proteggere le comunicazioni client tra un&#39;applicazione o un server di programmatore e i servizi Adobe Pass. Il flusso del DCR è separato, dipendente e flusso dei prerequisiti e si trova in [Registrazione client dinamica](/help/authentication/dynamic-client-registration.md).


### Autenticazione (authN)

Il flusso di autenticazione viene utilizzato per consentire a un utente di identificarsi nel proprio MVPD per determinare se l&#39;utente dispone di un account valido. 

1. L’utente avvia l’app Streaming Device e tenta di accedere o visualizzare contenuto protetto.
2. L&#39;app Streaming Device invia una richiesta al Servizio Programmatori per determinare se il dispositivo è già autenticato.
3. Il Servizio programmatori registra l&#39;app utilizzando il DCR.
4. Il Servizio programmatori controlla lo stato di autenticazione del dispositivo in streaming chiamando il servizio Adobe Pass **controllo** API.
5. Per il caso in cui **controllo** La chiamata restituisce lo stato di autenticazione del dispositivo utente, quindi l’app può procedere al flusso di autorizzazione.
6. Per il caso in cui **controllo** La chiamata restituisce lo stato di NON autenticazione del dispositivo utente, quindi l&#39;app deve attendere che una richiesta dell&#39;utente effettui l&#39;accesso.
7. Quando l’utente richiede l’accesso diretto (ad esempio seleziona il pulsante di accesso) o indiretto (ad esempio seleziona il contenuto protetto quando non è già autenticato), l’app Streaming Device invia una richiesta al Servizio programmatori per avviare l’autenticazione dell’utente. Il Servizio programmatori richiede e riceve un codice di registrazione univoco (regcode) chiamando il Servizio Adobe Pass **regcode** API.
8. Il servizio programmatore recupera anche l&#39;elenco degli MVPD e degli attributi correnti chiamando il servizio Adobe Pass **config** API. Nota: questa API può anche essere chiamata prima nel flusso e nella cache.
9. Il Servizio programmatori restituisce il codice regcode all&#39;app Streaming Device e all&#39;elenco MVPD elaborato richiesto nel passaggio \#7. Nota: Il formato dell&#39;elenco MVPD elaborato è specificato dal programmatore e può essere filtrato per consentire o bloccare esplicitamente MVPD specifici (cioè elenchi consentiti o blocchi).
10. Se è diverso dal dispositivo AuthN (ovvero &quot;secondo schermo&quot;), sia per scelta che per necessità (cioè il dispositivo di streaming non supporta un agente utente), il dispositivo di streaming deve visualizzare il codice regcode e un URI per l&#39;utente per accedere all&#39;applicazione AuthN. L&#39;utente digita l&#39;URI nell&#39;agente utente sul dispositivo AuthN per avviare l&#39;applicazione AuthN, quindi digita il codice regcode in tale applicazione. Se il dispositivo di streaming è lo stesso del dispositivo AuthN, il codice regcode può essere trasmesso programmaticamente al modulo AuthN.
11. Il modulo AuthN avvia l&#39;autenticazione utente con l&#39;MVPD visualizzando un selettore MVPD. Dopo che l&#39;utente seleziona l&#39;MVPD, il modulo AuthN chiama **autenticare** con il regcode, che reindirizza l&#39;agente utente all&#39;ID MVPD. Quando l&#39;utente si autentica correttamente con l&#39;MVPD, l&#39;agente utente viene reindirizzato attraverso il servizio Adobe Pass, dove l&#39;autenticazione corretta viene registrata con il codice regcode, e viene quindi reindirizzato al modulo AuthN.
12. Se il dispositivo di streaming è diverso dal dispositivo AuthN, il dispositivo AuthN deve visualizzare un messaggio di autenticazione all&#39;utente e i passaggi per continuare (ad esempio &quot;Success\! È ora possibile tornare alla console dei giochi per continuare \[...\]&quot;). Se il dispositivo di streaming è lo stesso del dispositivo AuthN, il dispositivo di streaming potrebbe rilevare programmaticamente il completamento dell&#39;autenticazione.

 

Il diagramma seguente illustra il flusso di autenticazione:

![](assets/authn-flow.png)

### Autorizzazione (authZ)

Il flusso di autorizzazione viene utilizzato per determinare se un utente ha il diritto di accedere al contenuto richiesto.

1. Ogni volta che l’utente tenta di visualizzare contenuto protetto nell’app Streaming Device, l’app Streaming Device chiama il Servizio programmatore che identifica il contenuto e richiede le autorizzazioni e le informazioni necessarie per avviare il flusso.
1. Il servizio programmatori chiama l&#39;Adobe Pass **autorizzare** Passaggio dell’API all’ID risorsa insieme ad altri parametri richiesti. Il servizio Adobe chiama il servizio MVPD AuthZ con l’ID risorsa e riceve e autorizza una decisione che viene quindi ritrasmessa al servizio programmatore. Questa decisione di autorizzazione verrà memorizzata nella cache dal servizio Adobe Pass per un periodo configurabile. In seguito **autorizzare** le chiamate dal servizio programmatore al servizio Adobe Pass, il valore memorizzato nella cache verrà restituito fintanto che è valido.
1. Se l&#39;autorizzazione viene concessa, il servizio programmatore deve chiamare l&#39;Adobe Pass **/tokens/media** API, che restituirà un token multimediale firmato. Il servizio programmatore deve convalidare il token multimediale utilizzando la libreria JAR (Media Token Verifier Library). Se valido, il Servizio programmatori deve restituire l&#39;autorizzazione e la richiesta di avviare il flusso (ad esempio l&#39;URL del flusso) richiesta nel passaggio \#1.
1. Se l&#39;autorizzazione è negata, il **autorizzare** La chiamata restituirà un codice di errore e una descrizione al Servizio programmatori. Il Servizio programmatori deve restituire il codice di errore e la descrizione (o un messaggio modificato dal programmatore) alla richiesta nel passaggio \#1.

Il diagramma seguente illustra il flusso di autorizzazione:

![](assets/authz-flow.png)

### Logout

Il flusso di logout consente a un utente di rimuovere l’identità attualmente associata all’applicazione.

1. Quando l&#39;utente richiede l&#39;logout (ovvero rimuove dal dispositivo l&#39;account MVPD corrente associato all&#39;applicazione), l&#39;app Streaming Device chiama il Servizio Programmatore e gli comunica di disconnettersi dal dispositivo.
1. Il servizio programmatore deve chiamare l&#39;Adobe Pass **disconnessione** API.

Il diagramma seguente illustra il flusso di logout:

![](assets/logout-flow.png)

### \[Facoltativo\] Preautorizzazione (anche nota come pre-volo)

La preautorizzazione può essere utilizzata per determinare rapidamente da un set di risorse quelle a cui un utente può accedere.  Il risultato di questa chiamata viene in genere utilizzato per personalizzare l’interfaccia utente di un singolo utente.

1. Una volta che l&#39;utente è autenticato, il dispositivo di streaming può chiamare il servizio programmatore per richiedere il contenuto a cui l&#39;utente ha diritto di trasmettere lo streaming.

1. Il servizio programmatore deve chiamare l&#39;Adobe Pass **preautorizzare** API con un elenco di ID risorsa, che sono una stringa semplice che in genere rappresenta un canale che un utente potrebbe avere diritto di inviare in streaming. *Nota: Attualmente, il* ***preautorizzare*** *La chiamata è configurata per limitare l’elenco a cinque (5) ID risorsa. Quando sono necessarie più di cinque risorse, più* ***preautorizzare*** *è possibile effettuare chiamate oppure configurare la chiamata per accettare più di cinque risorse con un accordo degli MVPD. Gli esecutori devono tenere presente il costo di un* ***preautorizzare*** *chiamare sia le risorse MVPD così come il tempo di risposta al programmatore e strutturare il loro uso della chiamata in modo giudizioso.*

1. La **preautorizzare** La chiamata risponderà al Servizio programmatori con un oggetto JSON contenente un valore TRUE o FALSE per ogni ID risorsa nella richiesta che indica se l&#39;utente ha diritto o meno al canale associato. *Nota: Se un MVPD non fornisce una risposta per un determinato ID risorsa (ad esempio a causa di errori di rete o timeout), il valore predefinito sarà FALSE.*

1. Il servizio programmatore deve utilizzare il **preautorizzare** chiama risposta per creare una risposta personalizzata definita dal programmatore al dispositivo di streaming, in genere per personalizzare la presentazione all&#39;utente in base alle sue adesioni.

Il diagramma seguente illustra il flusso di preautorizzazione:

![](assets/preauthz-flow.png)


### Metadati \[Facoltativo\]

I metadati possono essere utilizzati per recuperare le informazioni utente condivise dall&#39;MVPD.
 Esempi di questo possono includere ID utente, codice postale e così via.

1. Una volta che l&#39;utente è autenticato, il servizio programmatore può chiamare l&#39;Adobe Pass **metadati utente** API per richiedere informazioni sull’utente autenticato.

1. La risposta includerà tutti i metadati disponibili per l’utente specificato. I campi specifici sono configurati separatamente per ogni integrazione Programmer/MVPD.

Il diagramma seguente illustra il flusso di preautorizzazione:

 

![](assets/user-metadata-api-preauthz.png)

 

## Ambienti e requisiti funzionali{#environments}

 

Un programmatore deve creare almeno due ambienti: uno per la produzione e uno per lo staging.


### Produzione

L&#39;ambiente di produzione deve essere altamente disponibile e scalato in modo appropriato per picchi grandi o inaspettati (ad esempio, sport live, news).

 

Il servizio Adobe Pass viene eseguito su più data center geograficamente distribuiti in tutti gli Stati Uniti.  Per ottenere il tempo di risposta migliore (ovvero la latenza più bassa) dal servizio Adobe Pass, il programmatore deve anche creare un&#39;infrastruttura di servizio simile geograficamente dislocata. 


Il servizio Programmatore dovrebbe limitare la cache DNS a un massimo di 30 nel caso in cui l&#39;Adobe debba reindirizzare il traffico. Ciò può verificarsi se un data center diventa non disponibile.\
 

Il programmatore deve fornire la gamma IP pubblica dell&#39;ambiente di produzione. Questi verranno inseriti in un elenco di IP consentiti nell’infrastruttura Adobe Pass per l’accesso e gestiti dai criteri di utilizzo equi delle API di Adobe.

### Staging

L’ambiente di staging può essere minimo, ma deve includere tutti i componenti di sistema e la logica di business. Deve funzionare in modo simile alla produzione e consentire versioni di prova al di fuori della produzione. Idealmente, l&#39;ambiente di gestione temporanea può essere collegato agli ambienti di test di Adobe Pass per l&#39;utilizzo da parte del programmatore, e per Adobe, quando necessario, in modo da fornire assistenza nei test e nella risoluzione dei problemi.

### Requisiti funzionali

Il servizio Programmatore deve trasmettere informazioni accurate di identificazione del dispositivo per il quale esegue i flussi. Inoltre, il servizio Programmatore deve passare l&#39;IP del dispositivo per il quale esegue i flussi (in un&#39;intestazione x-inoltrata-per) insieme alla porta di origine della connessione (nel campo informazioni dispositivo):

    **X-Forwarded-For : \&lt;client _ip=&quot;&quot;>** 
    
    dove \&lt;client _ip=&quot;&quot;> è l’indirizzo IP pubblico del client
    
     
    
    L’intestazione deve essere aggiunta alle chiamate **regcode** e **autorizza**
    
    Esempi :
    
    POST /reggie/v1/{req\_id}/regcode HTTP/1.1
    
    X-Forwarded-For:203.45.101.20
    
     
    
    GET /api/v1/autorizzare HTTP/1.1
    
    X-Forwarded-For:203.45.101.20

 

Il servizio Programmatore deve inviare i dati e la formattazione richiesti da singoli MVPD o applicazioni integrate (ad esempio IP del dispositivo, porta sorgente, informazioni sul dispositivo, MRSS, dati facoltativi come ECID). <!--Please see the documentation for [Passing Device and Connection Information Cookbook](http://tve.helpdocsonline.com/passing-device-information-cookbook)-->.


Il servizio Programmatore deve rispettare i TTL authN e authZ quando vengono memorizzate nella cache e invalidare le sessioni authN o authZ quando vengono notificate.

Il programmatore deve mantenere i certificati condivisi con l&#39;Adobe.

<!--
## Related Information {#related}

* [REST API Reference](/help/authentication/rest-api-reference.md)
* [Glossary of Terms](/help/authentication/adobe-pass-glossary.md)
-->