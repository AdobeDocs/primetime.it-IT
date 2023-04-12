---
title: Funzioni di integrazione MVPD
description: Funzioni di integrazione MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 2%

---


# Funzioni di integrazione MVPD

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#mvpd-int-features-overview}

L&#39;autenticazione Adobe Primetime supporta gli standard emergenti per TV Everywhere. È conforme alla **Specifica di CableLabs OLCA (Online Content Access)**, che fornisce requisiti tecnici e architettura per la distribuzione di video a un cliente Pay TV da fonti online. L&#39;Adobe ha partecipato al progetto congiunto di test interopt CableLabs nel giugno 2011 e ha superato il processo di test per un&#39;implementazione Service Provider.  Adobe è anche un membro attivo del **OATC (Consorzio tecnico di autenticazione aperta)** e partecipa a diversi progetti di elaborazione delle specifiche dei sottocomitati nell&#39;ambito di tale organismo.

Dopo aver descritto la conformità di Primetime Authentication OLCA e la partecipazione del Adobe a OATC, è anche importante notare che l&#39;autenticazione di Primetime è in realtà &quot;agnostica del protocollo&quot;.  Ma in questa fase dell&#39;era TVE, l&#39;autenticazione Primetime è decisamente orientata verso gli standard OLCA.  Gli standard delineano i modi attualmente concordati per i diversi giocatori TVE (programmatori, MVPD e Service Provider) per implementare le funzioni TVE. Molte di queste funzioni sono elencate nelle tabelle seguenti, con collegamenti alle pagine correlate che forniscono dettagli ed esempi su come implementare le funzioni.

Le informazioni nelle tabelle sono destinate a guidare il processo di integrazione dell’autenticazione di Primetime verso funzionalità coerenti per tutte le integrazioni MVPD. La colonna di priorità classifica le funzioni in A, B e C:

* A - Queste sono funzionalità &quot;devono avere&quot; per l’implementazione iniziale di un’integrazione.
* B : questi sono importanti miglioramenti all’integrazione iniziale, da aggiungere dopo il rollout iniziale.
* C: sono ulteriori miglioramenti all’integrazione che possono essere implementati dopo i requisiti &quot;B&quot;.


## 1. Caratteristiche funzionali di base {#core-func-features}


| No. | Funzione | Descrizione | Priorità | Note |
|------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.1 | [Accesso avviato dal programmatore](/help/authentication/authn-oauth2-protocol.md) | Il visualizzatore seleziona l&#39;MVPD e avvia il flusso di autenticazione (AuthN) dal sito web o dall&#39;applicazione del marchio Programmer. | A+ |  |
| 1.2 | [Autorizzazione basata su canale](/help/authentication/authz-usecase.md) | Una volta autenticata, l&#39;autorizzazione (AuthZ) può verificarsi in background, con il passaggio all&#39;MVPD solo di un identificatore del canale di rete e di un identificatore utente. | A+ |  |
| 1.3 | Persistenza UserID | Il MVPD fornisce un UserID offuscato e persistente. | A |  |
| 1.4 | [Supporto per accesso singolo](/help/authentication/sso-support.md) | Il visualizzatore effettua l’accesso con l’MVPD sul sito di un marchio e può quindi passare a un altro marchio senza ricevere la richiesta di effettuare nuovamente l’accesso. La sessione AuthN è condivisa tra i marchi. Il supporto SSO è sia per i siti web che per le applicazioni mobili/dispositivi.  Per gli MVPD, richiede la restituzione di un ID utente o di un altro token utente che può essere utilizzato per AuthZ tra i marchi. | A |  |
| 1.5 | Esperienza utente di accesso ottimizzata per il dispositivo (UX) | L&#39;MVPD supporta il ridimensionamento della schermata di accesso in modo che si adatti alle dimensioni del dispositivo utilizzato dalla visualizzazione. | A |  |
| 1.6 | Logo predefinito del selettore MVPD | L’MVPD fornisce un URL a un logo predefinito di dimensioni appropriate (112x33 pixel). | A | Il logo deve essere ospitato dall’MVPD e deve essere memorizzato nella cache da CDN. |
| 1.7 | [Ambito del fornitore di servizi](/help/authentication/serv-provider-scoping.md) | MVPD supporta il passaggio dell’identificatore del marchio (valore Requestor) nella richiesta AuthN. | A- | Questo consente un&#39;esperienza di accesso specifica per il fornitore di servizi. |
| 1.8 | [Autorizzazione a più canali](/help/authentication/mvpd-preflight-authz.md#preflight-multich-authz) | L&#39;MVPD supporta un programmatore che invia più canali in un&#39;unica richiesta di autorizzazione. | B+ |  |
| 1.9 | Autenticazione basata su iFrame o &quot;JS Pop-up&quot; | Il programmatore è in grado di integrare il flusso di accesso in un&#39;esperienza iFrame o pop-up invece di un reindirizzamento HTTP. | B |  |
| 1.10 | [Logout avviato dal programmatore](/help/authentication/usecase-mvpd-logout.md) | Il visualizzatore dispone di una sessione autenticata sia sul sito o sull&#39;app del programmatore che con l&#39;MVPD. Il visualizzatore può avviare un logout federato dal sito del programmatore, e il logout cancella anche la sessione sul portale MVPD. | B | Assicura che i computer condivisi siano più protetti dall&#39;uso improprio dal punto di vista del programmatore. |
| 1.11 | [Messaggistica di errore di autorizzazione personalizzata](/help/authentication/error-reporting.md) | L&#39;MVPD passa la propria stringa di errore personalizzata, appropriata per la visualizzazione all&#39;utente del sito federato o dell&#39;app del programmatore. | B | Consente scenari di upselling |
| 1.12 | **Metadati utente nella risposta di autenticazione** | La risposta MVPD AuthN può includere metadati utente che fungono da suggerimento per la personalizzazione dell&#39;esperienza dell&#39;utente durante il flusso di adesione. Questo requisito consente ai suggerimenti di controllo genitori dal MVPD al programmatore. | B- |  |
| 1.13 | Autenticazione avviata da MVPD | Il visualizzatore completa una sessione AuthN di successo sul portale MVPD, quindi passa al sito TVE del programmatore. All&#39;utente non viene richiesto il selettore MVPD e viene autenticato automaticamente. | B- |  |
| 1.14 | Ambito ID utente | L&#39;UserID MVPD deve essere presente in due moduli: uno con ambito per i programmatori e l&#39;altro con ambito a livello di Adobe per le frodi.  Questo consente ad Adobe di condividere l&#39;UserID MVPD con ambito programmatore senza ulteriori crittografia/offuscamento. | C |  |
| 1.15 | Autorizzazione basata su risorse | Una volta completato AuthN, AuthZ può accadere in background, passando dati strutturati che possono includere rete, show, asset, valutazione di controllo dei genitori, e altro in base alle esigenze. Questo consente i controlli parentali su ogni chiamata AuthZ dal programmatore al MVPD. | C |  |
| 1.16 | Logout avviato da MVPD | Il visualizzatore dispone di una sessione autenticata sia sul sito o nell&#39;app del programmatore che con l&#39;MVPD. Il visualizzatore può avviare un logout federato dal sito dell&#39;MVPD che cancella anche la sessione su tutti i siti del programmatore federato. | C |  |
| 1.17 | Obblighi di autorizzazione | L&#39;MVPD fornisce condizioni aggiuntive nella risposta AuthZ, come la registrazione, o una classificazione di controllo massimo per genitori aggiornata (OLCA). | C |  |
| 1.18 | Contesto dell&#39;indirizzo IP | L&#39;MVPD richiede esplicitamente il passaggio dell&#39;indirizzo IP. Per AuthZ, dove le chiamate sono lato server, questo fornisce all&#39;MVPD informazioni di tracciamento delle frodi su dove l&#39;utente proviene dalla chiamata AuthZ. | C |  |
| 1.19 | Valore TTL (Time-to-live) del token definito in modo dinamico | L’MVPD è in grado di impostare il TTL del token di autenticazione Primetime in modo dinamico attraverso le proprietà nella risposta, in modo che l’Adobe sia fuori dal ciclo per le modifiche TTL. | C- |  |
| 1.20 | Tipo di dispositivo | L&#39;MVPD supporta il passaggio del tipo di dispositivo nella richiesta AuthN o AuthZ. Questa proprietà informa l&#39;MVPD della natura del dispositivo in cui verrà consumato il contenuto, in modo che possa regolare il TTL del token AuthN o AuthZ in modo che sia conforme alle proprie considerazioni di sicurezza per il dispositivo. | C- | Questo è utile per la piattaforma senza client, dove può essere difficile esporre ogni tipo di dispositivo come impostazione di configurazione sul lato dell&#39;autenticazione Primetime. |



## 2. Caratteristiche operative {#operational-features}

| No | Funzione | Descrizione | Priorità | Note |
|-----|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|-------|
| 2.1 | 24/7 Up-time | Un accordo MVPD per cercare di aumentare il tempo di 24/7 e misurare rispetto a quello nel tempo. | A |  |
| 2.2 | Credenziali Di Test Per Ciascun Programmatore | L&#39;MVPD fornisce account di test separati per ciascun programmatore. | A |  |
| 2.3 | Piano di scadenza del certificato e pianificazione del rinnovo | Un piano documentato MVPD con una pianificazione per garantire che i certificati SAML siano aggiornati. | A- |  |
| 2.4 | Latenza Media INFERIORE A 250 Ms / REAZIONE | Un accordo MVPD per lottare per una bassa latenza, e per misurarlo con quello nel tempo. | A- |  |
| 2.5 | Logo dell&#39;hosting del selettore MVPD | L&#39;MVPD deve ospitare il proprio logo e deve essere protetto dalla memorizzazione in cache CDN. | B |  |
| 2.6 | Piano di scalabilità del supporto | Un piano documentato MVPD per l&#39;escalation che è tenuto aggiornato e rivisto almeno trimestralmente. | A |  |
| 2.7 | Piano di protezione contro le interruzioni | Un piano MVPD con Adobe sulle misure di degradazione che può essere utilizzato in generale secondo necessità. | B |  |
| 2.8 | Gestisci endpoint di staging e produzione separati | Un test di integrazione MVPD che non richiede lo spoofing dei file host per testare l&#39;integrazione di staging. | B |  |
| 2.9 | Endpoint di controllo qualità aggiuntivi | L&#39;MVPD mantiene un&#39;integrazione QA IdP aggiuntiva per lo sviluppo di nuove funzioni congiunte.  Supportando questo passaggio, risulterebbe meno probabile che siano necessarie richieste speciali UAT per il test del certificato dell’app store. | C |  |





## 3. Funzioni di esperienza di autenticazione {#authn-exp-features}


| No | Funzione | Descrizione | Priorità | Note |
|-----|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 3.1 | Conversione autenticazione oltre le aspettative minime | L&#39;MVPD assicura un tasso di conversione minimo per dimostrarsi funzionale (5%) e ragionevole (30%). | A |  |
| 3.2 | Recupero password in linea | L&#39;MVPD fornisce un mezzo per recuperare le password in linea con il flusso federated AuthN. | A |  |
| 3.3 | Registrazione account in linea | L&#39;MVPD fornisce un mezzo per creare un nuovo conto in linea al flusso AuthN federato. | A |  |
| 3.4 | Guida in linea / Supporto | L&#39;MVPD fornisce un mezzo per fornire aiuto durante il flusso AuthN federato. | A |  |
| 3.5 | Autenticazione interna basata su modem | L&#39;MVPD autentica automaticamente un dispositivo quando si trova sulla rete locale di un modello registrato (solo ISP MVPD). | B | Questa è una priorità inferiore perché è un&#39;ottimizzazione che molti non possono ancora supportare e introduce alcune sfide per la riduzione delle frodi e i controlli dei genitori |
È ora possibile importare il codice della tabella Markdown direttamente utilizzando la finestra di dialogo File/Incolla dati della tabella...



## 4. Funzioni di Analytics {#analytics-features}


| No | Funzione | Descrizione | Priorità |
|-----|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| 4.1 | Allineamento funnel di conversione autenticazione | L&#39;MVPD ha una metrica per le richieste AuthN che inizia con la richiesta SAML AuthN - per allinearsi con le metriche di richiesta AuthN di Primetime Authentication e Programmer. | A |
| 4.2 | Utenti univoci | Utenti che sono stati autenticati correttamente e deduplicati in un rollup mensile tra giorni. | A |
| 4.3 | Contabilità del fuso orario | I rapporti includono il fuso orario in cui si ripete il giorno. | A |





## 5. Funzioni di attenuazione delle frodi {#fraud-mitgn-features}


| No | Funzione | Descrizione | Priorità | Note |
|-----|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------|
| 5.1 | Convalida del Sottoscrittore video durante l&#39;autenticazione | L&#39;MVPD assicura che l&#39;utente sia un utente con sottoscrizione video valida durante il flusso AuthN. | A |  |
| 5.2 | Limite di velocità per autenticazione/autorizzazione | L&#39;MVPD supporta la limitazione dei servizi Web per limitare l&#39;utilizzo da un account utente specifico quando appropriato. | B |  |
| 5.3 | UserID persistente con ambito globale da Adobe | L&#39;MVPD assicura che l&#39;Adobe abbia un UserID che può essere monitorato tra i programmatori per frode. Questo non deve essere fornito direttamente al cliente. | B | Specifiche del protocollo OMAP (Online Multimedia Authorization Protocol) e del monitoraggio degli utenti reali (RUM). |
| 5.4 | Convalida dell&#39;utilizzo simultaneo | L&#39;MVPD dispone di un mezzo per monitorare e limitare l&#39;utilizzo simultaneo dell&#39;account dell&#39;utente iscritto oltre una soglia aziendale. | B |  |

## P1. Funzioni specifiche dei proxy {#proxy-sp-func-features}

| No | Descrizione | Priorità | Note |
|-------|--------------------------------------------------------------------------------|----------|---------------------------------------------------|
| P 1,1 | Proxy incaricato di mantenere l&#39;accuratezza dell&#39;elenco aggiornato dei subMVPD | A |  |
| P 1,2 | Il proxy fornisce un logo di dimensioni appropriate per ogni subMVPD | A | Alcuni subMVPD live non hanno la giusta dimensione del logo |
| P 1,3 | Il proxy fornisce una pagina di accesso con marchio appropriato per ogni SubMVPD | A |  |
| P 1,4 | Proxy responsabile per il targeting di marchi specifici di fornitori di servizi con elenco subMVPD | B |  |
| P 1,5 | Proxy specifica correttamente tutte le proprietà subMVPD (dimensioni iFrame, TTL, logo, ecc.) | A |  |
| P 1,6 | Proxy specifica entityID separato | B |  |

## P2 Funzioni operative proxy {#proxy-op-features}

| No | Descrizione | Priorità |
|-------|----------------------------------------------------------------------------------------|----------|
| P 2,1 | Chiave API protetta | A |
| P 2,2 | Verificare le credenziali per il primo subMVPD utilizzato nell&#39;integrazione in tempo reale per ogni nuovo richiedente | A |
| P 2,3 | gli elenchi subMVPD sono accurati e completi per richiedente | A |
