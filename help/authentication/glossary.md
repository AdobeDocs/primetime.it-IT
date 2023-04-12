---
title: Glossario
description: Glossario
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Glossario {#glossary}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## AccessEnabler {#accessEnabler}

Il componente client dell’autenticazione Adobe Primetime. L’autenticazione Adobe Primetime fornisce una libreria AccessEnabler per ogni piattaforma supportata.

## AuthN {#authn}

Utilizzato come abbreviazione per &quot;authentication&quot;, come in &quot;AuthN Token&quot; o &quot;AuthN Flow&quot;.


## Token AuthN{#authn-token}

Token di autenticazione, generato dall’autenticazione Adobe Primetime dopo che un utente è stato autenticato con un MVPD. A seconda della piattaforma di integrazione del programmatore, il token viene memorizzato sul dispositivo dell’utente o sui server di autenticazione di Adobe Primetime.

## AuthZ {#authz}

Utilizzato come abbreviazione per &quot;autorizzazione&quot;, come in &quot;Token AuthZ&quot; o &quot;Flusso AuthZ&quot;.

## Token AuthZ {#authz-token}

Token di autorizzazione, generato dall’autenticazione Adobe Primetime dopo che un utente è stato autorizzato a visualizzare il contenuto protetto. Il token AuthZ viene memorizzato sui server di autenticazione Adobe Primetime e viene utilizzato per generare un [Token multimediale di breve durata](#short-lived-token).

## ID canale (obsoleto) {#channel_id}

Termine precedente per ID risorsa.

## API senza client {#clientless-api}

Una soluzione di integrazione di autenticazione Adobe Primetime che utilizza i servizi web invece del componente client AccessEnabler.

## ID dispositivo {#device-id}

Identifica in modo univoco un dispositivo (ad esempio un telefono, un tablet, ecc.) all’interno dell’autenticazione Adobe Primetime. Questo ID viene ottenuto / fornito dall&#39;applicazione del programmatore.


## Flusso di adesione{#entitlement_flow}

Il termine utilizzato nella documentazione di autenticazione di Adobe Primetime per fare riferimento all&#39;intero processo di registrazione di un dispositivo/utente con autenticazione Adobe Primetime, autenticazione di un utente con un MVPD, autorizzazione di una risorsa per un utente e disconnessione di un utente.


## GUID {#guid}

Vedi [ID utente](#user-id).

## IdP {#idp}

Identificare il fornitore; sinonimo di MVPD nel contesto del ruolo di un MVPD in un’integrazione di autenticazione Adobe Primetime. (I clienti devono verificare la propria identità tramite la pagina di accesso del provider di Pay TV.)

## Verificatore token multimediale {#media-token-verifier}

Libreria fornita da un Adobe utilizzata dai programmatori per verificare il token multimediale di breve durata generato dall&#39;autenticazione Adobe Primetime dopo il completamento di un flusso di adesione.

## MVPD {#mvpd}

Distributore di programmi video multicanale; sinonimo di &quot;Pay TV Provider&quot;.

## ID MVPD {#mvpd-id}

Vedi [ID utente](#user-id).

## ID partner {#partner-id}

Un identificatore che viene trasmesso in Adobe agli MVPD, che lo utilizzano per identificare per conto del quale l’autenticazione Adobe Primetime richiede l’autenticazione. A volte viene utilizzato per configurare le loro interfacce utente per particolari programmatori, a volte è lo stesso in tutti i programmatori, dipende dalle esigenze del MVPD.

## Provider TV a pagamento {#pay-tv-provider}

Sinonimo di [MVPD](#mvpd).

## Programmatore {#programmer}

Sinonimo di &quot;fornitore di contenuti&quot;, &quot;account&quot;, &quot;canale&quot;, &quot;fornitore di servizi&quot;, &quot;marchio&quot; e così via.

## MVPD proxy {#proxy-mvpd}

MVPD che fornisce servizi di identità per altri MVPD; direttamente integrato con l’autenticazione Adobe Primetime.

## MVPD proxy {#proxied-mvpd}

Un MVPD che non ha un&#39;integrazione diretta con l&#39;SP di Adobe, ma è integrato tramite un MVPD proxy.

## ID richiedente {#requestor-id}

Identifica in modo univoco un [Programmatore](#programmer) (un account, un marchio, un canale o una proprietà) nell’autenticazione Adobe Primetime. Questo ID è determinato tra il programmatore e l&#39;Adobe durante la configurazione iniziale dell&#39;account. Sul web, l’ID del richiedente è associato a un set di domini inseriti nella whitelist; tutte le chiamate che utilizzano un ID da un dominio esterno verranno rifiutate. I programmatori utilizzano anche l’ID del richiedente per l’analisi. In genere esiste un solo ID richiedente per programmatore. Una funzionalità aggiuntiva relativa all’ID richiedente è che il programmatore deve fornire ad Adobe un certificato pubblico, in quanto la chiamata API setRequestor prevede l’invio di dati crittografati, utilizzati per autenticare il programmatore nel sistema di autenticazione Adobe Primetime.

## ID risorsa {#resource-id}

Una stringa o una risorsa mRSS che identifica un [Programmatore](#programmer) agli MVPD. è concordato tra il programmatore e gli MVPD; L’autenticazione Adobe Primetime passa l’ID risorsa senza essere toccato, quindi deve essere lo stesso per tutti gli MVPD. Un programmatore può utilizzare più ID di risorse purché gli MVPD siano consapevoli di ciò che ogni ID rappresenta.

## SessionGUID {#sessionGUID}

Vedi [ID utente](#user-id).

## Token multimediale di breve durata {#short-lived-token}

Questo token viene generato dall&#39;autenticazione Adobe Primetime al completamento del processo di adesione per un particolare utente. Il token viene passato al programmatore, che utilizza il verificatore dei token di autenticazione di Adobe Primetime sul token di autenticazione breve per verificare la sicurezza del processo di adesione.

## Dispositivo avanzato {#smart-device}

Termine utilizzato in tutta la documentazione di autenticazione di Adobe Primetime per fare riferimento a set-top box, console giochi e smart TV. Si tratta di dispositivi con funzionalità di rete ma che non sono in grado di eseguire il rendering di pagine web.

## SP{#sp}

Fornitore di servizi; si riferisce solitamente al *ruolo* di SP, eseguito da Adobe Primetime Authentication, che agisce per conto di un programmatore in un&#39;integrazione con un [MVPD](#mvpd).

## Passaggio Temp {#temp-pass}

Funzione che consente ai programmatori di fornire un accesso temporaneo e gratuito al contenuto a pagamento. L&#39;accesso è per richiedente, per un periodo di tempo specificato dal programmatore.

## TTL {#ttl}

È Ora Di Vivere. Indica il periodo di tempo specificato per la validità di un token.

## TVE {#tve}

Televisione Ovunque.

## ID utente {#user-id}

Identifica in modo univoco l&#39;utente dell&#39;app di un programmatore, ma proviene dall&#39;MVPD. Disponibile in diversi moduli per diversi casi d’uso. Vedi [Informazioni sugli ID utente nella panoramica del programmatore](/help/authentication/programmer-overview.md#user-ids).

## Elenco Consentiti {#whitelist}

Un elenco di domini dichiarati legittimi ai fini della comunicazione con l’autenticazione Adobe Primetime.

## Token XSTS {#xsts-token}

Un token di sicurezza rilasciato da Microsoft per lo sviluppo di app per console Xbox, utilizzato nell&#39;integrazione di autenticazione Xbox/Adobe Primetime.
