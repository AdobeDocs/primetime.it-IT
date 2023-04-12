---
title: Dynamic Client Registration Management
description: Dynamic Client Registration Management
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---


# Dynamic Client Registration Management {#dynamic-client-registration-management}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Con l&#39;adozione diffusa di [Schede personalizzate Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target_blanck} e [Controller di visualizzazione Apple Safari](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target_blanck} nelle applicazioni dei nostri clienti, stiamo aggiornando il flusso di autenticazione utente in Adobe Primetime Authentication. Più specificamente, non possiamo più raggiungere l&#39;obiettivo di mantenere lo stato in modo che il flusso dell&#39;agente utente di autenticazione di un abbonato MVPD possa essere tracciato tra i reindirizzamenti. Questa operazione è stata eseguita in precedenza utilizzando i cookie HTTP. Questo limite è il driver per iniziare a migrare tutte le API a OAuth 2.0 [RFC6749](https://tools.ietf.org/html/rfc6749){target_blanck}.

Con questo aggiornamento, i client di autenticazione di Adobe diventano client OAuth 2.0 e viene distribuito un server di autorizzazione OAuth 2.0 personalizzato per soddisfare le esigenze del servizio di autenticazione di Adobe Primetime.

Affinché le applicazioni client utilizzino l’autorizzazione OAuth 2.0, il server deve registrarsi in modo dinamico per ottenere informazioni specifiche (credenziali client) per poter interagire con esso. Come parte del processo di registrazione, il client deve presentare un set di metadati incorporati all&#39;endpoint di registrazione client.

Questi metadati vengono comunicati come un&#39;istruzione software, che contiene un &quot;software_id&quot; per consentire al nostro server di autorizzazione di correlare diverse istanze di un&#39;applicazione utilizzando la stessa istruzione software.

A **dichiarazione del software** è un JSON Web Token (JWT) che dichiara valori di metadati sul software client come bundle. Se presentata al server di autorizzazione come parte di una richiesta di registrazione del client, l&#39;istruzione software deve essere firmata digitalmente o MAC utilizzando JSON Web Signature (JWS).

Puoi trovare una spiegazione più dettagliata su cosa sono le dichiarazioni software e come funzionano nella documentazione ufficiale [RFC7591](https://tools.ietf.org/html/rfc7591).

L&#39;istruzione software deve essere distribuita con l&#39;applicazione sul dispositivo dell&#39;utente.

Prima di questo aggiornamento, disponevamo di due meccanismi per consentire alle applicazioni di eseguire chiamate all’autenticazione Adobe Primetime:

* i client basati su browser sono registrati tramite [elenco di domini](/help/authentication/programmer-overview.md#reg-and-init)
* i client delle applicazioni native, come iOS e le applicazioni Android, sono registrati tramite **richiedente firmato** meccanismo


Con il meccanismo di autorizzazione Registrazione client, è necessario aggiungere le applicazioni al dashboard TVE.

Affinché un cliente possa iniziare a implementare il nuovo SDK per Android e l&#39;imminente SDK per iOS, deve disporre di un&#39;istruzione software. Un&#39;istruzione software identifica un&#39;applicazione creata nel Dashboard TVE.

Segui i passaggi descritti nelle sezioni seguenti per creare un&#39;applicazione registrata nel dashboard TVE.

## Creare un&#39;applicazione registrata {#create_app}

Sono disponibili due modi per creare un&#39;applicazione registrata nel dashboard TVE:

* [Livello del programmatore](#prog-level) - consente di creare un&#39;applicazione registrata e collegarla a uno o tutti i canali del programmatore.

* [Livello del canale](#channel-level) - consente di creare un&#39;applicazione registrata collegata in modo permanente solo a questo Canale.

### Creare un&#39;applicazione registrata a livello di programmatore {#prog-level}

Vai a **Programmatori** > **Applicazioni registrate** scheda .

![](assets/reg-app-progr-level.png)

Nella scheda Applicazioni registrate fare clic su **Aggiungi nuova applicazione**. Compila i campi richiesti nella nuova finestra.

Come illustrato di seguito, i campi da compilare sono i seguenti:

* **Nome applicazione** - il nome della domanda

* **Assegnato al canale** - il nome del canale, t</span>a cui è collegata questa applicazione. L’impostazione predefinita nella maschera a discesa è **Tutti i canali.** L’interfaccia ti consente di selezionare un canale o tutti i canali.

* **Versione applicazione** - per impostazione predefinita, è impostato su &quot;1.0.0&quot;, ma ti invitiamo vivamente a modificarlo con la tua versione dell’applicazione. Come best practice, se si decide di modificare la versione dell’applicazione, è consigliabile crearne una nuova.

* **Piattaforme di applicazione** - le piattaforme per l&#39;applicazione con cui collegare. È possibile selezionarli tutti o più valori.

* **Nomi di dominio** - i domini dell’applicazione con cui collegare. I domini nell’elenco a discesa sono una selezione unificata di tutti i domini da tutti i canali. Puoi selezionare più domini dall’elenco. Il significato dei domini è URL di reindirizzamento [RFC6749](https://tools.ietf.org/html/rfc6749). Nel processo di registrazione del client, l&#39;applicazione client può richiedere di poter utilizzare un URL di reindirizzamento per la finalizzazione del flusso di autenticazione. Quando un&#39;applicazione client richiede un URL di reindirizzamento specifico, questo viene convalidato in base ai domini inseriti nella whitelist in questa applicazione registrata associata all&#39;istruzione software.


![](assets/new-reg-app.png)


Dopo aver compilato i campi con i valori appropriati, fai clic su &quot;Fine&quot; per salvare l’applicazione nella configurazione.

Attenzione: **nessuna opzione per modificare un&#39;applicazione già creata**. Nel caso in cui si scopra che qualcosa creato non soddisfa più i requisiti , sarà necessario creare e utilizzare una nuova applicazione registrata con l&#39;applicazione client di cui soddisfa i requisiti.


### Registra una nuova applicazione a livello di canale {#channel-level}

Per creare un&#39;applicazione registrata a livello di canale, accedi al menu &quot;Canali&quot; e scegli quella per la quale desideri creare un&#39;applicazione. Quindi, dopo aver navigato alla scheda &quot;Applicazioni registrate&quot;, fare clic sul pulsante &quot;Aggiungi nuova applicazione&quot;.

![](assets/reg-new-app-channel-level.png)

Come mostrato di seguito, ciò che è leggermente diverso qui, rispetto alla stessa azione eseguita a livello di programmatore, è il menu a discesa &quot;Canali assegnati&quot; che non è abilitato, quindi non c&#39;è alcuna opzione per associare l&#39;applicazione registrata a un altro canale.

![](assets/new-reg-app-channel.png)

## Elencare applicazioni {#list-reg-app}

Dopo aver creato l&#39;applicazione registrata c&#39;è la possibilità di ottenere una dichiarazione software per presentare il server di autorizzazione come parte di una richiesta.

Per farlo, vai al Programmatore o al Canale per il quale sono state create le applicazioni registrate, dove sono elencate. 

Come illustrato di seguito , ogni voce dell’elenco sarà identificata da un nome, una versione e dei simboli per le piattaforme a cui è stata associata.

![](assets/reg-app-list.png)

Per ognuna di esse puoi :

* [Visualizza](#view)
* [Scaricare un&#39;istruzione software](#download-statement)

### Visualizza un&#39;applicazione registrata {#view}

Nell&#39;elenco delle applicazioni, sceglierne una e cliccando sul pulsante &quot;Visualizza&quot; verranno mostrati i dettagli utilizzati al momento della creazione. Come accennato in precedenza, non è possibile modificare nulla.


![](assets/view-reg-app.png)


### Scarica la dichiarazione del software {#download-statement}

Facendo clic sul pulsante &quot;Scarica&quot; sulla voce dell&#39;elenco per la quale è necessaria un&#39;istruzione software, verrà generato un file di testo. Questo file conterrà qualcosa di simile all&#39;output di esempio seguente.


![](assets/download-software-statement.png)

Il nome del file viene identificato in modo univoco tramite il prefisso &quot;software_statement&quot; e l’aggiunta della marca temporale corrente.

Si prega di notare che, per la stessa applicazione registrata, verranno ricevute diverse istruzioni software ogni volta che si fa clic sul pulsante di download, ma questo non invalida le istruzioni software precedentemente ottenute per questa applicazione. Questo accade perché vengono generati in loco, in base alla richiesta di azione.

Ce n&#39;è uno **limitazione** relativa all’azione di download. Se viene richiesta un&#39;istruzione software facendo clic sul pulsante &quot;Scarica&quot; poco dopo la creazione dell&#39;applicazione registrata e questo non è stato ancora salvato e il json di configurazione non è stato sincronizzato, il seguente messaggio di errore apparirà nella parte inferiore della pagina. 

![](assets/error-sw-statement-notready.png)

Questo racchiude un codice di errore HTTP 404 non trovato ricevuto dal core perché l&#39;id dell&#39;applicazione registrata non è ancora stato propagato e il core non ne è a conoscenza.

Dopo la creazione dell&#39;applicazione registrata, la soluzione è attendere al massimo 2 minuti per la sincronizzazione della configurazione. Dopo questo accade il messaggio di errore non sarà più ricevuto e il file di testo con l&#39;istruzione software sarà disponibile per il download.

Per informazioni dettagliate sul funzionamento del processo end to end o per ottenere informazioni su come vengono eseguite le richieste e quali risposte attese, consulta il collegamento in Informazioni correlate riportato di seguito, insieme ad altri collegamenti utili.

<!--
## Related Information {#related}

* [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
* [TVE Dashboard User Guide](/help/authentication/tve-dashboard-user-guide.md)
-->

## Demo delle funzioni {#tutorial}

Guarda [questo webinar](https://my.adobeconnect.com/pzkp8ujrigg1/) che offre più contesto delle funzioni e contiene una demo su come gestire le istruzioni software utilizzando la dashboard TVE e come testare quelle generate utilizzando un’applicazione demo fornita da Adobe come parte dell’SDK per Android.
