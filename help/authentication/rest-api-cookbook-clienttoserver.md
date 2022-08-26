---
title: Guida di riferimento API REST (da client a server)
description: Rest del client di cookie API sul server.
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 1%

---


# Guida di riferimento API REST (da client a server) {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica {#overview}

Questo documento fornisce istruzioni dettagliate affinché il team di progettazione di un programmatore possa integrare un &quot;dispositivo intelligente&quot; (console giochi, app Smart TV, set top box, ecc.) con autenticazione Adobe Primetime tramite i servizi REST API. Questo approccio da client a server, che utilizza API REST anziché un SDK client, consente un supporto più ampio di piattaforme diverse per le quali lo sviluppo di un numero significativo di SDK univoci non sarebbe fattibile. Per un&#39;ampia panoramica tecnica del funzionamento della soluzione Clientless, vedi [Panoramica tecnica senza client](/help/authentication/rest-api-overview.md).


Questo approccio richiede due componenti (app streaming e app AuthN) per completare i flussi richiesti: avvio, registrazione, autorizzazione e flussi di visualizzazione multimediale nell’app streaming e il flusso di autenticazione nell’app AuthN.

## Componenti {#components}

In una soluzione funzionante Client-to-Server sono coinvolti i seguenti componenti:

 

| Tipo | Componente | Descrizione |
| --- | --- | --- |
| Dispositivo di streaming | App in streaming | L&#39;applicazione Programmer che risiede sul dispositivo di streaming dell&#39;utente e riproduce il video autenticato. |
|  | Modulo AuthN \[Optional\] | se il dispositivo di streaming dispone di un agente utente (ad es. browser Web), il modulo AuthN è responsabile dell&#39;autenticazione dell&#39;utente sull&#39;IdP MVPD. |
| \[Facoltativo\] Dispositivo AuthN | App AuthN | se il dispositivo di streaming non dispone di un agente utente (ad es. browser Web), l&#39;applicazione AuthN è un&#39;applicazione Web Programmer a cui si accede dal dispositivo di un utente separato utilizzando un browser web.  |
| Infrastruttura Adobe | Servizio Adobe Pass | Un servizio che si integra con MVPD IdP e AuthZ Service e fornisce decisioni di autenticazione e autorizzazione. |
| Infrastruttura MVPD | IdP MVPD | Endpoint MVPD che fornisce un servizio di autenticazione basato su credenziali per convalidare l&#39;identità dell&#39;utente. |
|  | Servizio MVPD AuthZ | Un endpoint MVPD che fornisce decisioni di autorizzazione in base alle sottoscrizioni dell&#39;utente, ai controlli genitori, ecc. |

 

I termini aggiuntivi utilizzati nel flusso sono definiti nella variabile [Glossario](http://tve.helpdocsonline.com/adobe-pass-glossary).

## Flussi{#flows}

### Registrazione client dinamica (DCR)

Adobe Pass utilizza il DCR per proteggere le comunicazioni client tra un&#39;applicazione o un server di programmatore e i servizi Adobe Pass. Il flusso del DCR è separato, dipendente e flusso dei prerequisiti e si trova qui: http://tve.helpdocsonline.com/dynamic-client-registration


### Flussi delle app per streaming (Smart Device)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/clientless_1st_screen_updated.PNG)

 

#### Flusso di avvio

1. L&#39;app viene avviata e caricata l&#39;interfaccia utente iniziale.

2. Ottieni/genera un ID dispositivo.

3. Esegui una chiamata di verifica dell’autenticazione per verificare se il dispositivo è già autenticato.  Ad esempio: [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. Se la `checkauthn` la chiamata ha esito positivo, procedi al flusso di autorizzazione dal passaggio 2 in poi.  Se non riesce, avvia il flusso di registrazione.

 

#### Flusso di registrazione

1. Ottieni un codice di registrazione e un URL da utilizzare per accedere alla tua app di accesso alla seconda schermata e presentali all&#39;utente:

   a) Invia una richiesta di POST al servizio Adobe Registration Code, passando un ID dispositivo con hash e un &quot;URL di registrazione&quot;.  Ad esempio: [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b) Presenta all&#39;utente il codice di registrazione e l&#39;URL restituiti.

   c. Chiedi all&#39;utente di passare a un dispositivo compatibile con il web, passa all&#39;URL e quindi inserisci il codice di registrazione.

 

#### Flusso di autorizzazione

1. L&#39;utente ritorna dall&#39;app a seconda schermata e preme il pulsante &quot;Continua&quot; sul dispositivo. In alternativa, è possibile implementare un meccanismo di polling per controllare lo stato di autenticazione, ma l’autenticazione di Adobe Primetime consiglia il metodo del pulsante Continua per il polling. <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> Ad esempio: [\&lt;sp _fqdn=&quot;&quot;>/api/v1/token/autenticazione](/help/authentication/retrieve-authentication-token.md)

2. Invia una richiesta di GET al servizio di autorizzazione di autenticazione di Adobe Primetime per avviare l’autorizzazione. Ad esempio: `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

- Se la risposta indica il successo: L&#39;utente dispone di un token AuthN valido E l&#39;utente è autorizzato a guardare il supporto richiesto (è presente un token AuthZ valido per questo utente).

- Se la risposta indica un errore: Esamina l’eccezione generata per determinare il relativo tipo (AuthN, AuthZ o altro):

   - Se si è verificato un errore AuthN, riavvia il flusso di registrazione.

   - Se si è verificato un errore AuthZ, l’utente non è autorizzato a guardare il supporto richiesto e deve essere visualizzato un messaggio di errore di qualche tipo.

   - Se si è verificato un altro errore (errore di connessione, errore di rete, ecc.) quindi mostrare all’utente un messaggio di errore appropriato.

 

#### Visualizza flusso multimediale

1. Scelte di contenuti multimediali presenti. L&#39;utente seleziona il supporto da visualizzare.

2. I media sono protetti?

   a) L&#39;app controlla se il contenuto multimediale è protetto.

   b) Se il contenuto multimediale è protetto, l’app avvia il flusso di autorizzazione (AuthZ) riportato sopra.

   c. Se il supporto non è protetto, riprodurlo per l&#39;utente.

3. Riprodurre il supporto.


### Flusso app di AuthN (secondo schermo)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/smart_dev_second_flow.png)

1. Ottieni un elenco di MVPD per questo utente. Ad esempio: [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. Avvia il flusso di autenticazione.  Ad esempio: [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. Controlla se l&#39;autenticazione è riuscita.  Ad esempio: [`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. Invia nuovamente l&#39;utente all&#39;app Smart Device per completare il flusso di autorizzazione.

 

## Piattaforma SSO {#platform-sso}

Alcune piattaforme forniscono supporto dedicato per Single Sign-On (SSO). I dettagli dell’implementazione sono disponibili per ciascuna piattaforma:

- [Apple SSO](http://tve.helpdocsonline.com/rest-api-apple-sso)
- Amazon SSO

## TempPass e Promozionale TempPass per API REST {#temppass}

Per le implementazioni TempPass e Promozionale TempPass in cui l’utente non è tenuto a immettere le credenziali, l’autenticazione può essere implementata direttamente nell’app in streaming. 

**Per utilizzare questa API, l’app in streaming deve assicurarsi dell’univocità dell’ID dispositivo, in quanto viene utilizzata per identificare il token, insieme ai dati aggiuntivi facoltativi.**


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/Free%20preview%20option.png?dc=201612071020-0)

### Informazioni correlate {#related}

- [Riferimento API REST](/help/authentication/rest-api-reference.md)
