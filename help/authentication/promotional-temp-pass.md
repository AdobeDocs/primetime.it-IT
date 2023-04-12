---
title: Passaggio temporaneo promozionale
description: Passaggio temporaneo promozionale
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---


# Passaggio temporaneo promozionale {#promotional-temp-pass}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Riepilogo delle funzioni {#feature-summary}

Promozionale Temp Pass consente ai programmatori di offrire accesso temporaneo ai contenuti protetti per gli utenti che non dispongono di credenziali account con un MVPD.

Promozionale Temp Pass è progettato per l&#39;esecuzione di campagne promozionali in cui un utente, dopo aver fornito informazioni di identificazione valide (ad esempio, indirizzo e-mail) al programmatore, sarà in grado di utilizzare un **numero predefinito di titoli VOD diversi per un periodo di tempo predefinito**.

>[!IMPORTANT]
>
>Adobe non memorizza dati personali (PII, Personally Identifiable Information). Pertanto, il programmatore deve impostare un hash sopra l’utente univoco fornito sulle API di autenticazione di Primetime.

Il Passo Temp Promozionale è costruito sopra [Passaggio Temp](/help/authentication/temp-pass.md) che include tutte le funzionalità Temp Pass.

Una volta superato il numero massimo predefinito di titoli VOD o il periodo di tempo predefinito, l’utente non sarà in grado di accedere al contenuto sullo stesso dispositivo o utilizzando le stesse informazioni di identificazione utente (ad esempio, l’indirizzo e-mail) fino a quando i token di autorizzazione non saranno cancellati dal server di autenticazione di Adobe Primetime.

>[!NOTE]
>
>Temp Pass fa parte del pacchetto Premium Workflow. Per utilizzare questa funzionalità, contatta il tuo rappresentante commerciale Primetime .

## Confronto di Temp Pass e Promozionale Temp Pass {#tp-ptp-comparison}

| Passaggio Temp | Passaggio temporaneo promozionale |
|----------------------------------|----------------------------------------------------------------------------------------|
| Accesso ai contenuti <ul><li>basato sul tempo</li></ul> | Accesso ai contenuti <ul><li>basato sul tempo</li><li>in base al numero di risorse</li></ul> |
| Protezione dell&#39;accesso basata su <ul><li>ID dispositivo</li></ul> | Sicurezza basata su <ul><li>ID dispositivo</li><li>hash sulle informazioni di identificazione utente fornite (ad esempio, e-mail)</li></ul> |
| API di errore client disponibile | API di errore client disponibile |
| Reimpostazione / Rimozione disponibile | Reimpostazione / Rimozione disponibile |

## Dettagli delle funzioni {#feature-details}

Questa funzione consente agli utenti di accedere ai contenuti promozionali da un dispositivo specifico (telefono e tablet) dopo aver fornito informazioni univoche, come l&#39;indirizzo e-mail, nell&#39;applicazione del programmatore.

Il programmatore fornirà un hash sui dati PII dell’utente sulle API di autenticazione e autorizzazione. Questo hash verrà utilizzato insieme all’ID dispositivo per generare una chiave univoca per identificare l’utente e il dispositivo.

In base all’ID dispositivo e alle informazioni fornite dall’utente e alla logica seguente, l’autenticazione Adobe Primetime determinerà se l’utente si trova in una nuova versione di prova o in una esistente:

* nuovo hash sulle informazioni fornite dall&#39;utente (ad esempio, e-mail), nuovo ID dispositivo => nuova versione di prova
* hash esistente su informazioni fornite dall’utente (ad esempio, e-mail), nuovo ID dispositivo => versione di prova esistente (con hash esistente su informazioni fornite dall’utente (ad esempio, e-mail)
* nuovo hash sulle informazioni fornite dall’utente (ad esempio, e-mail), ID dispositivo esistente => versione di prova esistente (con ID dispositivo esistente)
* hash esistente su informazioni fornite dall&#39;utente (ad esempio, e-mail), ID dispositivo esistente => versione di prova esistente

>[!NOTE]
>La convalida e l&#39;hashing delle informazioni fornite dall&#39;utente vengono gestite dal programmatore, non dall&#39;Adobe.

**La funzione Promozionale Temp Pass può essere configurata in base alle seguenti proprietà:**

* Chiave informazioni fornita dall’utente (ad esempio e-mail)
* Numero di risorse che l’utente ha diritto di utilizzare
* TTL : l’intervallo di tempo entro il quale l’utente ha diritto a utilizzare il numero configurato di risorse

### Metadati utente {#user-metadata}

Per facilitare l&#39;attuazione dell&#39;applicazione del Programmatore, **le informazioni sui metadati dell&#39;utente sono esposte** sul Passo Temp Promozionale, con le chiavi corrispondenti (per attivare le chiavi, contattare tve-support@adobe.com):

* **rimanenti_risorse**: il numero di risorse rimanenti che l&#39;utente corrente ha diritto di utilizzare
* **used_assets**: elenco delle risorse già utilizzate dall&#39;utente corrente
* **expiration_date**: la data di scadenza dell’utente corrente

### Come viene calcolato il tempo di visualizzazione? {#compute-viewing-time}

Il tempo di validità di un passaggio temporaneo non è correlato al tempo impiegato dall&#39;utente per la visualizzazione del contenuto nell&#39;applicazione del programmatore. Alla richiesta iniziale di autorizzazione da parte dell’utente tramite Promotional Temp Pass, viene calcolato un tempo di scadenza aggiungendo il tempo iniziale di richiesta corrente al TTL (periodo di tempo) specificato dal Programmatore.

### Autenticazione e autorizzazione {#authn-authz}

Per i flussi di transito temporaneo promozionale, l&#39;autenticazione e l&#39;autorizzazione non comunicano con un MVPD effettivo, **in modo che tutte le richieste di autorizzazione abbiano esito positivo** purché siano soddisfatte tutte queste condizioni:

* i token di autorizzazione sono validi per le risorse specificate
* numero di **used_assets** è inferiore al limite fissato dal programmatore
* **expiration_date** è successivo alla data corrente.

### Comportamento della verifica preliminare {#preflight-beh}

Quando viene effettuata una richiesta di preflight o preautorizzazione per un MVPD di Passaggio temporaneo promozionale, la risposta di Preflight corrispondente restituita conterrà l&#39;intero elenco di risorse della Richiesta di verifica preliminare come verifica preliminare riuscita.

La logica alla base di ciò è: le condizioni di autorizzazione per il passaggio temporaneo promozionale si basano sul limite di tempo e di numero di risorse anziché su risorse specifiche. In particolare, purché il vincolo di tempo sia soddisfatto e il limite di risorse non venga superato, le risorse richiamate saranno autorizzate.

### SSO {#sso}

L&#39;SSO non è abilitato per le istanze di Promozionale Temp Pass, che è configurato con &quot;Authentication Per Requestor&quot; abilitato. Ciò significa che quando l&#39;utente passa dall&#39;applicazione A a un&#39;altra applicazione B integrata con lo stesso Temp Pass promozionale, l&#39;utente non verrà connesso automaticamente.

### Logout {#logout}

Tutti i token su un dispositivo vengono eliminati al momento del logout. Pertanto, il passaggio da Promozionale Temp Pass a un MVPD regolarmente selezionato dall’utente non dovrebbe basarsi su questa implementazione. Si consiglia di utilizzare la `setSelectedProvider(null)` per cancellare lo stato dell&#39;applicazione e quindi riavviare il flusso di autenticazione, che ha una migliore esperienza utente.

### Diagramma di flusso del passaggio temporaneo promozionale {#promo-tempass-flowdia}

![Diagramma di flusso del passaggio temporaneo promozionale](assets/promo-temp-pass-flow.png)

*Figura: Flusso promozionale del passaggio temporaneo*

## Implementare il passaggio temporaneo promozionale {#impl-promo-tempass}

Il passaggio temporaneo promozionale richiede le seguenti funzionalità lato client:

* **Informazioni sull’identificatore utente, ad esempio la propagazione dell’indirizzo e-mail** (invio dell&#39;indirizzo e-mail dell&#39;utente sui flussi di autenticazione e autorizzazione). L’e-mail è necessaria per l’autenticazione Adobe Primetime al fine di associare i token di autenticazione e autorizzazione (simile al caso del `device_ID`, obbligatorio per tutte le chiamate).
* **Forza autenticazione** - consente al programmatore di forzare un flusso di autenticazione quando l&#39;utente è già autenticato. Questa funzionalità è necessaria per forzare l&#39;aggiornamento dei metadati dell&#39;utente (la chiave dei metadati dell&#39;utente) **used_assets** contiene il numero di risorse disponibili) ogni volta che l&#39;app viene avviata. Poiché l&#39;utente può effettuare l&#39;accesso su più dispositivi, i metadati utente presenti sul dispositivo durante l&#39;avvio dell&#39;app non sono affidabili e dobbiamo aggiornarli in modo da riflettere lo stato corrente per quell&#39;utente specifico (identificato dall&#39;indirizzo e-mail).


>[!IMPORTANT]
>L’autenticazione forzata è possibile solo su iOS e Android.
>L’autenticazione di Primetime non dispone di un meccanismo integrato per arrestare lo streaming gratuito dopo che gli X minuti sono passati. L&#39;autenticazione di Primetime cesserà l&#39;emissione **autorizzazione** e **media breve** token una volta che l’utente utilizza le risorse Y gratuite. Spetta ai programmatori limitare l&#39;accesso una volta che il passaggio temporaneo promozionale scade.

## Sicurezza {#security}

>[!IMPORTANT]
>Adobe non memorizza dati personali (PII, Personally Identifiable Information). Pertanto, il programmatore deve impostare un hash sopra l’utente univoco fornito sulle API di autenticazione di Primetime.

**Hashing delle informazioni sull’identificatore utente**

L&#39;Adobe consiglia di utilizzare **SHA-2** familiare o la sua **SHA-256**, **SHA-512** funziona sui dati prima dell&#39;invio ad Adobe.

Ad esempio: **SHA-256** over **&quot;user@domain.com&quot;** è **&quot;f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&quot;**.

## Ripristino o eliminazione del passaggio temporaneo promozionale {#reset-promo-tempass}

Alcune regole aziendali richiedono un&#39;eliminazione regolare del pass temporaneo promozionale. Per farlo, Primetime Authentication fornisce ai programmatori un *pubblico* API web, descritta di seguito:

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>Protocollo: **https**</li><li>Host:<ul><li>Versione: **mgmt.auth.adobe.com**</li><li>Prerequisito: **mgmt-prequal.auth.adobe.com**</li></ul></li><li>Percorso: **/reset-tempass/v2/reset**</li><li>Parametri query: **device_id=all&amp;requestor_id=THE_REQUESTOR_ID&amp;mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>intestazioni: ApiKey: **1232293681726481**</li> <li>Risposta:<ul><li>Operazione riuscita: **HTTP 204**</li><li>Errore: **HTTP 400** per richieste errate, **HTTP 401** se ApiKey non è specificato, **HTTP 403** se ApiKey non è valido</li></ul></li></ul> |

Oltre ai requisiti per eliminare Temp Pass, il Passaggio temporaneo promozionale utilizza l’hash sulle informazioni dell’identificatore utente inviate come **generic_data** sull&#39;autenticazione e l&#39;autorizzazione per l&#39;eliminazione.

L’hash verrà inviato, non l’intero JSON:

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"
```

### Client supportati {#supported-clients}

| Client di autenticazione Adobe Primetime | Passaggio temporaneo promozionale | Ripristina strumento | Supporta codice di risposta dedicato / Errore client |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| Abilitatore di accesso JS | SÌ | SÌ | SÌ (a partire dalla versione 3.0.0) |
| iOS client nativo | SÌ | SÌ | SÌ (a partire dalla versione 1.10) |
| Android client nativo | SÌ | SÌ | SÌ |
| API senza client | SÌ | SÌ | NO |


## Limitazioni {#limitations}

Questa sezione descrive le limitazioni applicabili all&#39;implementazione corrente di Promozionale Temp Pass.

### Clientless {#lim-clientless}

**Dispositivi avanzati senza ID dispositivo univoco**

Non tutte le app per dispositivi avanzati sono in grado di fornire un ID dispositivo univoco. In mancanza di uno, l’autenticazione Adobe Primetime può utilizzare l’UUID generato dal servizio Adobe per il codice di registrazione come ID dispositivo univoco. Ciò significa che quando l’utente si disconnette, i token di autenticazione e autorizzazione verranno eliminati. Una volta che l&#39;utente tenterà nuovamente di eseguire l&#39;autenticazione, questa volta con informazioni utente diverse (ad esempio, e-mail) l&#39;utente sarà in grado di autorizzare nuovamente. Adobe consiglia di aggiungere un flusso di interfaccia utente che non consenta a un utente di &quot;ingannare&quot; il sistema e di aggiungere logica per determinare se si tratta di un nuovo utente che richiede una versione di prova o una versione di prova esistente.

**Ripristino/eliminazione di Temp Pass**

Reset Temp Pass per Clientless non è disponibile nei casi specifici di Xbox360 e Xbox One, perché queste piattaforme richiedono l&#39;analisi aggiuntiva degli ID dispositivo, non possibile nello strumento Reset Temp Pass .

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->