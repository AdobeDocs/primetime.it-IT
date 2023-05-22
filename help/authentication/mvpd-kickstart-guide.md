---
title: Piano di integrazione diretta MVPD
description: Piano di integrazione diretta MVPD
exl-id: 6423cc9a-a45a-4cde-b562-4cb72c98e505
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Guida introduttiva MVPD: piano di integrazione diretta MVPD {#mvpd-dir-int-plan}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#mvpd-kickstart-intro}

Ti diamo il benvenuto nell’autenticazione Adobe Primetime per TV Everywhere.  Saremo lieti di collaborare con voi.

>[!NOTE]
>
>Questa è la Guida Kick-Start per gli MVPD (Multichannel Video Programming Distributors). Se sei un programmatore (provider di contenuti), consulta [Guida di Kick-Start per programmatori](/help/authentication/programmer-kickstart-guide.md).

Il supporto è sempre disponibile tramite il sistema di ticket di autenticazione Primetime su Zendesk. Qui puoi anche trovare esempi, documentazione e tutorial video per i nostri processi. Per utilizzare [Zendesk](https://adobeprimetime.zendesk.com/), dovrai registrarti e creare un account su https://tve.zendesk.com/home. Non esiste alcun limite alla quantità di utenti che è possibile registrare e che possono visualizzare o pubblicare commenti su un ticket archiviato. Tutte le domande di supporto devono essere indirizzate a: tve-support all&#39;indirizzo adobe.com

**Contatti team**:

**Supporto** - Per tutte le domande, i problemi o le richieste di funzioni **tve-support@adobe.com**.

## 1. Riunioni di avvio {#kickoff-meetings}

L&#39;ambito di tali riunioni è l&#39;avvio di discussioni tecniche tra l&#39;Adobe e l&#39;MVPD. A questo punto, la documentazione deve essere condivisa da entrambe le parti. Come follow-up, Adobe deve aprire un ticket nel nostro sistema di ticket (https://tve.zendesk.com/) per monitorare lo stato dell’integrazione.

## 2. Caratteristiche {#features}

Adobe imposterà una chiamata di stato settimanale per discutere e monitorare la pianificazione complessiva, i passaggi, la tempistica e i dettagli di implementazione dell’integrazione. In questa fase, Adobe esegue una revisione delle specifiche MVPD. Il risultato dovrebbe essere una pagina delle specifiche che descriva tutte le funzioni necessarie per MVPD. Il MVPD invierà all&#39;Adobe un documento di specifica, che descrive l&#39;autenticazione / implementazione dell&#39;autorizzazione del MVPD.

Elementi da chiarire, vedi [Funzioni di integrazione MVPD](/help/authentication/mvpd-integr-features.md).

A questo punto è necessario descrivere in dettaglio diverse impostazioni:

* **URL del logo MVPD** - Questo è un file con le seguenti dimensioni: 112 x 33 pixel. Il logo viene visualizzato dai programmatori sui loro siti quando l&#39;utente fa clic sul pulsante &quot;Accedi&quot; per selezionare il provider di Pay TV.
* **Valori TTL (time-to-live)** - Il TTL viene in genere impostato dal MVPD durante il processo di autenticazione/autorizzazione. Tuttavia, Adobe può ignorare tali valori TTL e fornire valori diversi a seconda di quanto concordato sia dal programmatore che dall’MVPD.
* **Nome visualizzato** - Questo viene visualizzato dai programmatori sui loro siti quando l&#39;utente fa clic sul pulsante &quot;Accedi&quot; per selezionare il proprio provider di Pay TV.
* **Credenziali di prova** - Entrambi i profili (staging e produzione) devono avere un elenco di credenziali di test.

>[!IMPORTANT]
>
>Ogni volta che un utente avvia un flusso di adesione, viene associato a un singolo ID utente, opaco e univoco.  L’ID utente viene utilizzato per identificare l’utente dell’app di un programmatore, ma ha origine dall’MVPD.

>[!CAUTION]
>
>Un avviso importante per ogni MVPD: l’ID utente NON deve contenere dati PII (personalmente identificabili), informazioni che possono essere utilizzate da sole o con altre informazioni per identificare, contattare o individuare l’utente.

## 2. Scambio di metadati {#metadata-ex}

Le due parti devono scambiarsi i metadati per tutti gli ambienti coinvolti (produzione, staging, ecc.).

* **Adobe**
   * Per l’ambiente di staging i metadati SP dell’Adobe possono essere recuperati da: [Metadati SP di staging autenticazione](https://sp.auth-staging.adobe.com/sp/metadata)
   * Per l&#39;ambiente di produzione, i metadati SP dell&#39;Adobe possono essere recuperati da: [Metadati SP di produzione per l’autenticazione](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * Aggiungere metadati (staging/produzione)

## 4. Elenco IP consentiti {#allow-ip-list}

I seguenti IP devono essere inseriti nella whitelist del firewall di MVPD. Per l’elenco degli IP, contatta l’Adobe.

* L’autenticazione Primetime richiede l’apertura di firewall sulle porte 80 e 443, per consentire l’accesso a risorse limitate.

* Il MVPD deve aggiungere un elenco di indirizzi IP per i server di autenticazione e autorizzazione (se questo è il caso).

## 5. Sviluppo {#deve}

La durata della fase di sviluppo sarà determinata dopo aver rivisto le specifiche e tenendo conto degli elementi su cui le due parti si impegnano. L&#39;Adobe deve scrivere un codice personalizzato per la parte di autorizzazione.

>[!NOTE]
>
>Tieni presente che l’autorizzazione viene eseguita per risorsa. La transazione di autorizzazione viene in genere eseguita con una stringa ID, passata dal sito del programmatore, che rappresenta il canale per il quale l’utente richiede l’autorizzazione. Questo ID risorsa viene stabilito tra il programmatore e MVPD e può essere tanto granulare quanto necessario.

## 6. Ambienti di Adobe {#adobe-env}

In questo Adobe vengono forniti ambienti diversi per le diverse fasi del processo di sviluppo:

* **Prequalificazione** (PRE-QUAL): L’ambiente PRE-QUAL contiene il candidato della versione successiva. Adobe integra inizialmente nuovi partner in questo ambiente, prima di aggiornare l’integrazione all’ambiente Release. I partner dispongono di due settimane per eseguire il test sull&#39;ambiente PRE-QUAL e devono richiedere esplicitamente eventuali modifiche alla configurazione PRE-QUAL (contattare il proprio rappresentante di Adobe per informazioni dettagliate sulla procedura di richiesta di modifica). Le correzioni di bug attivano nuove distribuzioni in questo ambiente.
* **Versione** (VERSIONE): l’attuale build di produzione di Adobe viene implementata in un ambiente live qui.

Per ulteriori informazioni su come utilizzare gli ambienti di Adobe, consulta [Informazioni sugli ambienti Adobe](/help/authentication/understanding-the-adobe-environments.md)

## 7. Distribuzione nell’ambiente di staging {#stag-env}

In base ai metadati ricevuti da MVPD, Adobe creerà e configurerà un nuovo MVPD nel sistema di autenticazione di Primetime. Questo verrà implementato nell’ambiente di staging precedente a Adobe e verrà configurato con il nostro programmatore di test (TestDistributors).

MVPD deve eseguire la stessa distribuzione nel proprio ambiente di QA/staging/test.

## 8. Test e risoluzione dei problemi {#tes-troubleshoot}

In questa fase, l’Adobe e il test MVPD e la risoluzione dei problemi di integrazione. Per facilitare il test dell’integrazione, il team di autenticazione di Primetime può utilizzare il sito di test API di Adobe. Per ulteriori informazioni sull’utilizzo del sito di test API di Adobe, consulta [Test dell’autenticazione e dei flussi di autorizzazione tramite il sito di test Adobe API](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

Quando il test e la risoluzione dei problemi sono terminati correttamente, l’integrazione viene abilitata nell’ambiente di staging di Adobe. A questo punto, Adobe può integrare MVPD con un programmatore effettivo.

## 9. Distribuzione di produzione {#prod-dep}

* Per testare la connettività, MVPD deve prima implementare nel profilo di produzione.

* Adobe distribuisce in prequal production.

* Tutte le parti possono ora eseguire il test nel profilo di produzione.

* Se a questo punto tutto è a posto, Adobe può spostare l’integrazione nell’ambiente di produzione della versione (&quot;live&quot;), che è disponibile per tutti gli utenti.

## 10. Procedure di riassegnazione {#esc-proc}

Una volta che l’integrazione è live in produzione, è fondamentale fornire la migliore esperienza del cliente. Per garantire la migliore risposta nel caso di un problema di inattività del server, gli MVPD devono fornire la documentazione della procedura di riassegnazione per i problemi portati all&#39;attenzione degli Adobi.

A sua volta, Adobe fornisce agli MVPD il processo di escalation dell’autenticazione Primetime più recente.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
