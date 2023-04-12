---
title: Piano di integrazione diretta MVPD
description: Piano di integrazione diretta MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Guida Kickstart MVPD: Piano di integrazione diretta MVPD {#mvpd-dir-int-plan}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#mvpd-kickstart-intro}

Benvenuti nell&#39;autenticazione Adobe Primetime per TV Everywhere.  Siamo ansiosi di lavorare con voi.

>[!NOTE]
>
>Questa è la Guida di Kickstart per i distributori MVPD (Multichannel Video Programming Distributor). Se sei un programmatore (provider di contenuti), consulta la [Guida Kickstart per programmatori](/help/authentication/programmer-kickstart-guide.md).

Il supporto è sempre disponibile attraverso il sistema di ticket di autenticazione Primetime su Zendesk. Qui puoi trovare anche campioni, documentazione e tutorial video per i nostri processi. Per utilizzare [Zendesk](https://adobeprimetime.zendesk.com/), dovrai registrarti e creare un account all’indirizzo https://tve.zendesk.com/home. Non vi è alcun limite alla quantità di utenti che puoi registrare e che possono visualizzare o pubblicare commenti su un biglietto archiviato. Tutte le domande di assistenza devono essere rivolte a: tve-support su adobe.com

**Contatti del team**:

**Supporto** - Per tutte le domande, gli incidenti o le richieste di funzioni **tve-support@adobe.com**.

## 1. Riunioni rapide {#kickoff-meetings}

L&#39;ambito di tali riunioni è l&#39;avvio di discussioni tecniche tra l&#39;Adobe e il MVPD. A questo punto del processo, la documentazione deve essere condivisa da entrambe le parti. Come follow-up, l&#39;Adobe deve aprire un ticket nel nostro sistema di ticket (https://tve.zendesk.com/) per tenere traccia dello stato dell&#39;integrazione.

## 2. Caratteristiche {#features}

In Adobe verrà impostata una chiamata di stato settimanale per discutere e tenere traccia della pianificazione generale, dei passaggi, della cronologia e dei dettagli di implementazione dell’integrazione. In questa fase, l&#39;Adobe effettua una revisione delle specifiche MVPD. Il risultato di questo dovrebbe essere una pagina specifica che descrive tutte le funzioni necessarie per l&#39;MVPD. L&#39;MVPD invierà ad Adobe un documento sulle specifiche, che descrive in dettaglio l&#39;implementazione di autenticazione/autorizzazione dell&#39;MVPD.

Articoli da chiarire, vedi [Funzioni di integrazione MVPD](/help/authentication/mvpd-integr-features.md).

A questo punto è necessario descrivere in dettaglio diverse impostazioni:

* **URL del logo MVPD** - Questo è un file con le seguenti dimensioni: 112 x 33 pixel Il logo viene visualizzato dai programmatori sui loro siti quando l&#39;utente fa clic sul pulsante &quot;Accedi&quot; per selezionare il proprio provider di Pay TV.
* **Valori TTL (time-to-live)** - Il TTL viene generalmente impostato dal MVPD durante il processo di autenticazione/autorizzazione. Tuttavia, l&#39;Adobe può ignorare questi valori TTL e fornire valori diversi a seconda di quanto concordato sia dal programmatore che dal MVPD.
* **Nome visualizzato** - Questo viene visualizzato dai programmatori sui loro siti quando l&#39;utente fa clic sul pulsante &quot;Accedi&quot; per selezionare il proprio provider di Pay TV.
* **Verificare le credenziali** - Entrambi i profili (staging e produzione) devono avere un elenco di credenziali di test.

>[!IMPORTANT]
>
>Ogni volta che un utente avvia un flusso di adesione, viene associato a un singolo ID utente univoco e opaco.  L&#39;ID utente viene utilizzato per identificare l&#39;utente dell&#39;app di un programmatore, ma proviene dall&#39;MVPD.

>[!CAUTION]
>
>Un avviso importante per ogni MVPD: l&#39;ID utente NON deve contenere informazioni PII (personalmente identificabili), informazioni che possono essere utilizzate da sole o con altre informazioni per identificare, contattare o individuare l&#39;utente.

## 2. Scambio di metadati {#metadata-ex}

Le due parti devono scambiare i metadati per tutti gli ambienti interessati (produzione, staging, ecc.).

* **Adobe**
   * Per l&#39;ambiente di gestione temporanea, i metadati SP dell&#39;Adobe possono essere recuperati da: [Metadati sp di staging dell&#39;autenticazione](https://sp.auth-staging.adobe.com/sp/metadata)
   * Per l&#39;ambiente di produzione, i metadati SP di Adobe possono essere recuperati da: [Metadati sp di produzione dell&#39;autenticazione](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * Per aggiungere metadati (staging/produzione).

## 4. Consenti elenco IP {#allow-ip-list}

I seguenti IP devono essere inseriti nella whitelist del firewall MVPD. Contattare l&#39;Adobe per l&#39;elenco degli IP.

* L’autenticazione di Primetime richiede l’apertura dei firewall sulle porte 80 e 443 per consentire l’accesso alle risorse limitate.

* L’MVPD deve aggiungere un elenco di indirizzi IP per i server di autenticazione e autorizzazione (se questo è il caso).

## 5. Sviluppo {#deve}

La durata della fase di sviluppo sarà determinata dopo aver riveduto le specifiche e tenuto conto dei punti sui quali le due parti firmano. L&#39;Adobe deve scrivere codice personalizzato per la parte di autorizzazione.

>[!NOTE]
>
>Tieni presente che l’autorizzazione viene eseguita per risorsa. La transazione di autorizzazione viene in genere eseguita con una stringa ID, trasmessa dal sito del programmatore, che rappresenta il canale per il quale l&#39;utente richiede l&#39;autorizzazione. Questo ID risorsa è stabilito tra il programmatore e MVPD e può essere granulare come necessario.

## 6. Ambienti di Adobe {#adobe-env}

Adobe fornisce ambienti diversi per diverse fasi del processo di sviluppo:

* **Prequalificazione** (PRE-QUAL): L’ambiente PRE-QUAL contiene il candidato per la versione successiva. Adobe integra inizialmente nuovi partner in questo ambiente, prima di aggiornare l’integrazione all’ambiente di rilascio. I partner dispongono di due settimane per testare l&#39;ambiente PRE-QUAL e devono richiedere esplicitamente qualsiasi modifica alla configurazione PRE-QUAL (contatta il tuo rappresentante di Adobe per i dettagli sul processo di richiesta delle modifiche). Le correzioni di bug attivano nuove distribuzioni in questo ambiente.
* **Versione** (RILASCIO): La build di produzione corrente di Adobe viene implementata in un ambiente live qui.

Per ulteriori informazioni sull’utilizzo degli ambienti Adobe, consulta [Informazioni sugli ambienti Adobe](/help/authentication/understanding-the-adobe-environments.md)

## 7. Distribuzione temporanea {#stag-env}

In base ai metadati ricevuti dall&#39;MVPD, Adobe creerà e configurerà un nuovo MVPD nel sistema di autenticazione Primetime. Questo verrà implementato nell&#39;ambiente di staging precedente di Adobe e sarà configurato con il nostro programmatore di test (TestDistributors).

L’MVPD deve eseguire la stessa implementazione nel proprio ambiente QA/staging/test.

## 8. Test e risoluzione dei problemi {#tes-troubleshoot}

In questa fase, l&#39;Adobe e il test MVPD e la risoluzione dei problemi dell&#39;integrazione. Per facilitare il test dell’integrazione, il team di autenticazione di Primetime può utilizzare il sito di test API di Adobe. Per ulteriori informazioni sull’utilizzo del sito di test API di Adobe, consulta [Test dei flussi di autenticazione e autorizzazione tramite il sito di test API di Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

Al termine dei test e della risoluzione dei problemi, l’integrazione viene abilitata nell’ambiente di gestione temporanea della versione di Adobe. A questo punto, l&#39;Adobe può integrare l&#39;MVPD con un programmatore effettivo.

## 9. Distribuzione della produzione {#prod-dep}

* Per testare la connettività, l’MVPD deve essere implementato per primo nel profilo di produzione.

* L&#39;Adobe viene implementato in produzione preuguale.

* Ora tutte le parti possono eseguire il test nel profilo di produzione.

* Se tutto va bene a questo punto, Adobe può spostare l’integrazione nell’ambiente di produzione della versione (&quot;live&quot;), disponibile per tutti gli utenti.

## 10. Procedure di scalatura {#esc-proc}

Una volta che l&#39;integrazione è in produzione, è fondamentale fornire la migliore esperienza del cliente. Per garantire la migliore risposta nel caso di un problema di inattività del server, gli MVPD devono fornire la documentazione della procedura di inoltro per i problemi portati all&#39;attenzione del Adobe.

A sua volta, Adobe fornisce agli MVPD il più recente processo di escalation di autenticazione Primetime.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
