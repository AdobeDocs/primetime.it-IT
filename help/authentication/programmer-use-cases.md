---
title: Casi d'uso del programmatore
description: Casi d'uso del programmatore
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---


# Casi d&#39;uso del programmatore {#programmer-use-cases}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Questo documento riepiloga i casi di utilizzo dell’integrazione del programmatore supportati dall’autenticazione Adobe Primetime. È possibile controllare questa pagina prima di iniziare un progetto di integrazione per vedere quali funzioni sono attualmente supportate.

## Casi d’uso {#use-cases}


### Integrazione di base: Autenticazione e autorizzazione federate per una rete a canale singolo {#basic-integration}

**Priorità** - Alta

**Suddivisione** - App TVE a marchio singolo a programmatore con una rete a 1 canale ospitata all’interno dell’esperienza

Questo consente ai programmatori di offrire contenuti premium, nella propria app TVE di marchio*, con un controllo federato dell&#39;adesione all&#39;MVPD. Il requestorID deve essere allineato in modo che corrisponda al marchio dell’applicazione che distribuisce il contenuto al visualizzatore. In questo scenario, esiste una relazione da 1 a 1 tra l’ID richiedente autenticazione Adobe Primetime e l’ID risorsa che viene verificato per l’adesione.

>[!NOTE]
>
>L’app TVE viene utilizzata in questo documento per fare riferimento collettivamente ai diversi tipi di applicazioni (applicazioni web, app mobili, ecc.) supportato dall’autenticazione Adobe Primetime. La colonna Piattaforme riportata di seguito può contenere dettagli sulle piattaforme supportate per casi d’uso specifici.

#### Casi d’uso specifici (comuni alla maggior parte delle integrazioni) {#sp-use-cases-basic-int}

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|:--------:|:-----------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:-----------------------------------------:|
| Alta | Individuazione MVPD dall&#39;app TVE del programmatore | L&#39;utente inizia sull&#39;app TVE con il marchio del programmatore e viene richiesto di selezionare il proprio provider MVPD. | API Clientless per web (SWF/JS) per dispositivi mobili (iOS/Android) (per 2° schermo) |  |
| Alta | Autenticazione federata dall’app TVE del programmatore | L&#39;utente inizia sull&#39;app TVE con il marchio del programmatore e dopo aver selezionato il proprio provider MVPD, l&#39;utente passa alla pagina di accesso del MVPD per inserire le proprie credenziali. | Web (SWF/JS) Mobile (iOS/Android) |  |
| Alta | Autorizzazione dall&#39;app TVE del programmatore | Dopo l&#39;autenticazione dell&#39;utente, l&#39;app TVE del programmatore è in grado di effettuare richieste di autorizzazione del back-channel all&#39;MVPD per controllare l&#39;adesione dell&#39;utente. Di solito si tratta solo di verificare se Channel Network è nel pacchetto di abbonamento MVPD degli utenti.                                  In questo caso, l’ID del richiedente e l’ID della risorsa corrispondono a 1:1. | Tutte le piattaforme |  |
| Media | Disconnessione dall&#39;app TVE del programmatore | Consente all’utente di disconnettersi e cancellare i token AuthN/AuthZ dell’autenticazione di Adobe Primetime. In molti casi, questo disconnette anche l&#39;utente dall&#39;MVPD. Ma gli MVPD variano a seconda che questo sia supportato. Cancella sempre la sessione e i token di autenticazione di Adobe Primetime. | Tutte le piattaforme eccetto XBox Native | Diversi MVPD non lo supportano. |
| Alta | Single Sign-On tra siti e app | Consente all&#39;utente di condividere la sessione di accesso tra siti e app senza dover ripetere l&#39;accesso. | Tutte le piattaforme eccetto API Clientless | Richiede almeno SDK 1.7 per alcuni MVPD. |

### App TVE singola che ospita più reti di canali {#single-app-multi-channel}

**Priorità**- Alta

Consente al programmatore di aggregare più reti di canali di contenuti sulla stessa destinazione del marchio per i propri visualizzatori.

#### Casi d’uso specifici {#sp-use-cases-singl-tve-app}

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Alta | Autorizzazione per canale distinto | L’utente è in grado di guardare contenuti provenienti da più reti di canali all’interno della stessa app TVE. Il programmatore è in grado di effettuare chiamate di autorizzazione specifiche per ogni rete di canale per confermare l&#39;adesione degli utenti. | Tutte le piattaforme | Tutti gli MVPD ora lo supportano in qualche forma. |
| Basso | Query di autorizzazione della verifica preliminare | Questo consente al programmatore di controllare quali canali l&#39;utente ha nel proprio pacchetto in una singola chiamata API. Questa operazione viene eseguita prima delle chiamate AuthZ effettive per filtrare il contenuto dall’interfaccia utente a cui l’utente non ha accesso. |  | La maggior parte degli MVPD non espone ancora questi dati come Attributi utente, quindi l&#39;Adobe effettua chiamate AuthZ per ottenerli. Inoltre, la maggior parte degli MVPD sono limitati a 5 alla volta, perché non supportano più canali in una singola chiamata.                             È molto importante verificare quanti canali il programmatore deve effettuare il controllo preliminare. Indipendentemente dal numero, dovremo verificare che sia corretto con gli MVPD. La maggior parte degli MVPD non supportano attualmente più di 5 canali (3° trimestre, 2013). |

### Autorizzazione a livello di risorsa {#asset-level-authz}

**Priorità** - Basso

**Suddivisione** - Passa Un Identificatore Di Risorsa Alla Richiesta Di Autorizzazione

**Piattaforme** - Tutte le piattaforme

#### Casi d’uso specifici {#sp-use-cases-asset-lvl-authz}

Abilita l’MVPD per ottenere l’analisi del livello delle risorse su ogni chiamata AuthZ. Questo ha lo svantaggio di negare la cache AuthZ di autenticazione Adobe Primetime.

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------|--------------------------------------|
| Basso | Passa un identificatore di risorsa sulla richiesta di autorizzazione | Abilita l’MVPD per ottenere l’analisi del livello delle risorse su ogni chiamata AuthZ.  Dispone del lato negativo della negazione della cache AuthZ di autenticazione di Adobe Primetime. | Tutte le piattaforme | Attualmente questo è supportato da un solo MVPD. |




### Controllo genitori {#parental-controls}

**Priorità** - Basso

Consente di applicare le restrizioni dell&#39;account utente MVPD sull&#39;app TVE del programmatore.

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------|
| Basso | Filtrare il contenuto in base agli attributi dell’utente | Consente al programmatore di controllare la valutazione massima consentita per un utente prima di eseguire il rendering dell&#39;elenco dei contenuti disponibili per l&#39;utente. | Web (Flash/JS) Mobile (iOS/Android) | Attualmente funziona solo con un MVPD. |
| Basso | Passa le valutazioni del contenuto nella richiesta AuthZ | Consente al programmatore di passare la valutazione specifica del contenuto che l’utente desidera visualizzare come parte della richiesta AuthZ all’MVPD correlato a #3, in quanto le valutazioni sono in genere a livello di risorsa. | Tutte le piattaforme | Attualmente funziona solo con un MVPD. |

#### Personalizzazione dell&#39;integrazione MVPD per marchio programmatore {#mvpd-int-cust-prog-brand}

**Priorità** - Media

Abilita l’esperienza personalizzata durante AuthN o per i messaggi di errore AuthZ.

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------|
| Media | Passa l&#39;identificatore del provider di servizi nella richiesta AuthN. | Abilitare il branding specifico nella pagina di accesso MVPD specifica per il provider di servizi. Abilita anche la selezione automatica del valore predefinito in modo che corrisponda al pubblico come Spagnolo per Univision. | Tutte le piattaforme | Varia per MVPD. Alcuni non lo supportano. |
| Media | Messaggi di errore personalizzati nella risposta di AuthZ | Abilita i messaggi di errore specifici del programmatore o del marchio dall&#39;MVPD che possono includere un messaggio specifico per l&#39;upselling con un collegamento che aggiorna il pacchetto. | Web, Android, iOS | Varia per MVPD. Alcuni non lo supportano. |


### Casi di utilizzo del dispositivo collegato {#connected-devices}

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Media | XBox LiveID SSO tra app e console | Consente all&#39;utente di condividere la sessione AuthN tra le app e tra diverse console di gioco, in base al proprio account LiveID. | SDK nativo XBox | La maggior parte degli MVPD non piace perché il modello tipico è quello di associare il token al dispositivo, non all&#39;utente.                             Se possibile, non raccomandiamo più questo approccio. |
| Alta | Dispositivo connesso con token associati all’appID sul dispositivo | Consente al programmatore di associare l&#39;adesione MVPD nel token all&#39;appID sul dispositivo a cui è stato emesso. | API senza client | In questo modo il dispositivo collegato si allinea più strettamente all’implementazione standard Pass per i token.                             Deve comunque essere migliorato per essere un ID a livello di dispositivo. |

### Lunghezza TTL AuthN specifica per il dispositivo {#authn-ttl-length}

Abilita l&#39;adesione TVE per eventi speciali che potrebbero non essere risorse nel database di adesione MVPD come canali normali.

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| Alta | Impostare valori TTL diversi per piattaforma | Consente al programmatore di stabilire una lunghezza TTL diversa per i dispositivi web, mobili e collegati. Al momento, l’autenticazione Adobe Primetime supporta la possibilità di avere 3 valori TTL separati: Web (Flash) Mobile/HTML5 Clientless - Dispositivi collegati |  | Alcuni MVPD impostano il TTL in modo dinamico. Se necessario, Adobe può ignorare queste impostazioni dinamiche utilizzando le impostazioni di configurazione. |

### Applicazioni speciali basate su eventi {#special-event}

**Priorità** - Basso

Abilita l&#39;adesione TVE per eventi speciali che potrebbero non essere risorse nel database di adesione MVPD come canali normali.

| Priorità | Caso d’uso | Descrizione | Piattaforme | Note MVPD |
|--------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------------------------|
| Basso | Canali multipli come proxy per un evento | Questo è stato fatto per le Olimpiadi, dove l&#39;abbonato doveva avere due canali diversi nel loro pacchetto per avere accesso. In questo caso, l’autenticazione Adobe Primetime ha creato un nuovo resourceID e ha fatto sì che tutti gli MVPD effettuino la mappatura ai canali specifici sul loro lato.  Ha funzionato bene con un preavviso sufficientemente avanzato. Questo era importante perché la maggior parte degli MVPD non supportano più chiamate di risorse. | Tutte le piattaforme | Supportato da tutti gli MVPD con un preavviso adeguato. |
| Basso | Nuova applicazione evento speciale, utilizzando le risorse del canale esistenti | Questo è stato fatto per March Madness. Il provider di contenuti ha creato una nuova app con un nuovo requestorID. Tutti gli MVPD necessari per aggiungere il supporto per il nuovo requestorID nel loro sistema. Gli resourceID erano canali normali.  Alcuni MVPD dovevano anche mappare i canali come validi in base al nuovo richiedente, quindi era necessario più tempo per quei casi. | Tutte le piattaforme | Supportato da tutti gli MVPD con un preavviso adeguato. |
| Basso | requestorID, resourceID esistente | Questo è stato fatto per il torneo del weekend di golf di Masters. È stato solo un piccolo evento per un paio di giorni, e i Maestri avevano la loro app mobile che era possibile mostrare il contenuto. Il programmatore ha pianificato di pagare il traffico di autenticazione di Adobe Primetime e di utilizzare il proprio requestorID standard e resourceID. L&#39;unico trucco era avere il programmatore condividere un certificato mobile per la firma requestorID con i master, e questo ha aggiunto alla loro configurazione come loro certificato di backup per quel fine settimana. | Tutte le piattaforme | Nessun impatto per gli MVPD |

### Integrazione del server dei contenuti {#content-server-integration}

**Priorità**- Media

Abilitazione della convalida del token multimediale prima del rilascio del flusso video al lettore client.
| Priorità | Caso d&#39;uso | Descrizione | Piattaforme | Note MVPD | |—|—|—|—|—|—| | Alto | Programmatore Federated Player - Con Autorizzazione A Livello Di Pagina | Le API di autenticazione Adobe Primetime vengono eseguite in JavaScript nella pagina e il token viene passato nel lettore. Il token può essere passato al servizio di convalida in un paio di modi: Ottieni parametro sul parametro URL del servizio di convalida trasmesso nella stringa query dell&#39;interfaccia esterna dell&#39;URL di flusso API FlashVars | | | | Media | Programmatore Federated Player - Con Autorizzazione Interna Del Lettore | Le API di autenticazione di Adobe Primetime vengono eseguite in ActionScript nel SWF player, quindi il token è disponibile per il lettore dal callback.                                                                                                                                                                                         | | | | Alto | Lettore sindacato - Ospitato sul portale MVPD con autorizzazione a livello di pagina utilizzando un iFrame per avvolgere il lettore | Simile al lettore con autorizzazione a livello di pagina, ma con il wrapper della pagina del lettore iFramed nel portale MVPD. L&#39;autenticazione deve avvenire separatamente nel portale MVPD.                                                                                                                                                    |           |                        |


<!--
>[!RELATEDINFORMATION]
>
>* MVPD Integration Features
>* Entitlement Flow
>* Platform / Device Requirements
-->
