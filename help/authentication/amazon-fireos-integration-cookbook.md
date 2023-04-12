---
title: Guida di riferimento per l’integrazione di Amazon FireOS
description: Guida di riferimento per l’integrazione di Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---


# Guida di riferimento per l’integrazione di Amazon FireOS {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>


## Introduzione {#intro}

Questo documento descrive i flussi di lavoro di adesione che un&#39;applicazione di livello superiore di un programmatore può implementare attraverso le API esposte dalla libreria Amazon FireOS AccessEnabler.

La soluzione di adesione all&#39;autenticazione Adobe Primetime per Amazon FireOS è infine divisa in due domini:

- Dominio dell&#39;interfaccia utente : si tratta del livello di applicazione superiore che implementa l&#39;interfaccia utente e utilizza i servizi forniti dalla libreria AccessEnabler per fornire accesso ai contenuti con restrizioni.
- Dominio AccessEnabler : in questo punto i flussi di lavoro di adesione vengono implementati sotto forma di:
   - Chiamate di rete effettuate ai server back-end di Adobe
   - Regole business-logic relative ai flussi di lavoro di autenticazione e autorizzazione
   - Gestione di varie risorse ed elaborazione dello stato del flusso di lavoro (come la cache dei token)

L&#39;obiettivo del dominio AccessEnabler è quello di nascondere tutte le complessità dei flussi di lavoro di adesione e fornire all&#39;applicazione di livello superiore (tramite la libreria AccessEnabler) un set di primitivi di adesione semplici con cui implementare i flussi di lavoro di adesione:

1. Imposta l&#39;identità del richiedente
1. Controllare e ottenere l&#39;autenticazione con un provider di identità specifico
1. Controllare e ottenere l&#39;autorizzazione per una particolare risorsa
1. Logout

L&#39;attività di rete di AccessEnabler si svolge in un thread diverso, pertanto il thread dell&#39;interfaccia utente non viene mai bloccato. Di conseguenza, il canale di comunicazione bidirezionale tra i due domini di applicazione deve seguire un pattern completamente asincrono:

- Il livello dell&#39;applicazione dell&#39;interfaccia utente invia messaggi al dominio AccessEnabler tramite le chiamate API esposte dalla libreria AccessEnabler.
- AccessEnabler risponde al livello dell&#39;interfaccia utente attraverso i metodi di callback inclusi nel protocollo AccessEnabler che il livello dell&#39;interfaccia utente registra con la libreria AccessEnabler.

## Flussi di diritto {#entitlement}

1. [Prerequisiti](#prereqs)
1. [Flusso di avvio](#startup_flow)
1. [Flusso di autenticazione](#authn_flow)
1. [Flusso di autorizzazione](#authz_flow)
1. [Visualizza flusso multimediale](#media_flow)
1. [Flusso di disconnessione](#logout_flow)

 

### A. Prerequisiti {#prereqs}

1. Crea le funzioni di callback:
   - [`setRequestorComplete()`](#$setRequestorComplete)

      - Attivato da `setRequestor()`, restituisce successo o errore.     Il successo indica che è possibile procedere con le chiamate di adesione.
   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      - Attivato da `getAuthentication()` solo se l&#39;utente non ha selezionato un provider (MVPD) e non è ancora autenticato. La `mvpds` è un array dei provider disponibili per l&#39;utente.
   - [`setAuthenticationStatus(status, reason)`](#$setAuthNStatus)

      - Attivato da `checkAuthentication()` ogni volta. Attivato da `getAuthentication()` solo se l&#39;utente è già autenticato e ha selezionato un provider.

      - Lo stato restituito è autenticato o non autenticato, il motivo descrive un errore di autenticazione o un&#39;azione di logout.
   - [navigaToUrl(url)](#$navigateToUrl)

      - Ignorato in AmazonFireOS SDK, il metodo viene utilizzato sulle piattaforme Android in cui viene attivato da `getAuthentication()` dopo che l&#39;utente ha selezionato un MVPD.  La `url` fornisce la posizione della pagina di login di MVPD.
   - [`sendTrackingData(event, data)`](#$sendTrackingData)

      - Attivato da `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
La `event` il parametro indica quale evento di adesione si è verificato;il `data` è un elenco di valori relativi all&#39;evento. 
   - [`setToken(token, risorsa)`](#$setToken)

      - Attivato da `checkAuthorization()` e `getAuthorization()` dopo aver ottenuto l’autorizzazione per visualizzare una risorsa.
      - La `token` è il token per contenuti multimediali di breve durata;il `resource` è il contenuto che l&#39;utente è autorizzato a visualizzare.
   - [`tokenRequestFailed(risorsa, codice, descrizione)`](#$tokenRequestFailed)

      - Attivato da `checkAuthorization()` e `getAuthorization()` dopo un&#39;autorizzazione non riuscita.
      - La `resource` parametro è il contenuto che l&#39;utente stava tentando di visualizzare; la `code` parametro è il codice di errore che indica il tipo di errore verificatosi; la `description` Il parametro descrive l&#39;errore associato al codice di errore.
   - [`selectedProvider(mvpd)`](#$selectedProvider)

      - Attivato da `getSelectedProvider()`.
      - La `mvpd` fornisce informazioni sul provider selezionato dall&#39;utente.
   - [`setMetadataStatus(metadati, chiave, argomenti)`](#$setMetadataStatus)

      - Attivato da `getMetadata().`
      - La `metadata` fornisce i dati specifici richiesti; la `key` è la chiave utilizzata nel `getMetadata()` richiesta; e `arguments` è lo stesso dizionario passato a `getMetadata()`.
   - [`preauthorizedResources(resources)`](#$preauthResources)

      - Attivato da `checkPreauthorizedResources()`.
      - La `authorizedResources` presenta le risorse che l&#39;utente è autorizzato a visualizzare.\
          










![](assets/android-entitlement-flows.png)\
 

### B. Flusso di avvio {#startup_flow}

1. Avvia l&#39;applicazione di livello superiore.
1. Avvia autenticazione Adobe Primetime
   1. Chiamata [`getInstance`](#$getInstance) per creare una singola istanza di Adobe Primetime authentication AccessEnabler.

      - **Dipendenza:** Libreria Adobe Primetime Authentication Native Amazon FireOS (AccessEnabler)
   2. Chiamata` setRequestor()` stabilire l&#39;identificazione del programmatore; trasmettere il `requestorID` e (facoltativamente) un array di endpoint di autenticazione Adobe Primetime.

      - **Dipendenza:** RequestorID di autenticazione di Adobe Primetime valido (puoi utilizzare Adobe Primetime Authentication Account Manager per organizzare questa operazione.)

      - **Triggers:** setRequestorComplete() callback

   Non è possibile completare nessuna richiesta di adesione finché il richiedente non ha stabilito completamente l&#39;identità. Ciò significa che, mentre setRequestor() è ancora in esecuzione, tutte le richieste di adesione successive (ad esempio,`checkAuthentication()`) sono bloccate.

   Sono disponibili due opzioni di implementazione: Una volta inviate le informazioni di identificazione del richiedente al server di back-end, il livello di applicazione dell&#39;interfaccia utente può scegliere uno dei due approcci seguenti:</p>

   1. Attendi l&#39;attivazione della `setRequestorComplete()` callback (parte del delegato di AccessEnabler).  Questa opzione offre la massima certezza che `setRequestor()` completato, quindi consigliato per la maggior parte delle implementazioni.

   1. Continua senza attendere l&#39;attivazione del `setRequestorComplete()` callback e avvio dell&#39;emissione di richieste di adesione. Queste chiamate (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) vengono messe in coda dalla libreria AccessEnabler, che effettuerà le chiamate di rete effettive dopo il `setRequestor()`. Questa opzione può essere interrotta occasionalmente se, ad esempio, la connessione di rete è instabile.




1. Chiamata [checkAuthentication()](#$checkAuthN) per verificare l&#39;esistenza di un&#39;autenticazione senza avviare il flusso completo di autenticazione.  Se questa chiamata ha esito positivo, puoi procedere direttamente al flusso Autorizzazione.  In caso contrario, procedi al flusso di autenticazione.

- **Dipendenza:** Chiamata riuscita a `setRequestor()` (questa dipendenza si applica anche a tutte le chiamate successive).

- **Triggers:** callback setAuthenticationStatus()

### C. Flusso di autenticazione {#authn_flow}

1. Chiamata [`getAuthentication()`](#$getAuthN) per avviare il flusso di autenticazione o per ottenere la conferma che l’utente è già autenticato. 

   **Triggers:**  

   - Il callback setAuthenticationStatus(), se l&#39;utente è già autenticato.  In questo caso, procedi direttamente al [Flusso di autorizzazione](#authz_flow).
   - Il callback displayProviderDialog(), se l&#39;utente non è ancora autenticato.  

1. Presentare all’utente l’elenco dei provider inviati a `displayProviderDialog()`.

1. Dopo che l&#39;utente seleziona un provider, viene aperta la pagina del provider per l&#39;accesso dell&#39;utente

   **Nota:** A questo punto, l&#39;utente ha l&#39;opportunità di annullare il flusso di autenticazione. In questo caso, AccessEnabler ne pulirà lo stato interno e reimposterà il flusso di autenticazione.

1. Dopo un accesso riuscito da parte dell&#39;utente, WebView verrà chiuso.

1. chiamare `getAuthenticationToken(),` che indica ad AccessEnabler di recuperare il token di autenticazione dal server back-end. 

1. [Facoltativo] Chiamata [`checkPreauthorizedResources(resources)`](#$checkPreauth) per verificare quali risorse l’utente è autorizzato a visualizzare. La `resources` è un array di risorse protette associato al token di autenticazione dell&#39;utente.\
   **Triggers:** `preAuthorizedResources()` callback\
   **Punto di esecuzione:** Dopo il flusso di autenticazione completato

1. Se l’autenticazione ha avuto esito positivo, procedi al flusso di autorizzazione.

 

### D. Flusso di autorizzazione {#authz_flow}

1. Chiamata [`getAuthorization()`](#$getAuthZ) avviare il flusso di autorizzazione.

   Dipendenza: ResourceID(s) valido(i) concordato con l&#39;MVPD(s).

   **Nota:** Gli ID risorsa devono essere gli stessi utilizzati su qualsiasi altro dispositivo o piattaforma e devono essere gli stessi negli MVPD.

1. Convalida autenticazione e autorizzazione.

   - Se la `getAuthorization()` la chiamata ha esito positivo: L’utente dispone di token AuthN e AuthZ validi (l’utente è autenticato e autorizzato a guardare il supporto richiesto).
   - Se `getAuthorization()` errore: Esamina l’eccezione generata per determinare il relativo tipo (AuthN, AuthZ o altro):
      - Se si è verificato un errore di autenticazione (AuthN), riavvia il flusso di autenticazione.
      - Se si è verificato un errore di autorizzazione (AuthZ), l’utente non è autorizzato a guardare il supporto richiesto e deve essere visualizzato un messaggio di errore di qualche tipo.
      - Se si è verificato un altro tipo di errore (errore di connessione, errore di rete, ecc.) quindi mostrare all’utente un messaggio di errore appropriato.

1. Convalida il token per contenuti multimediali brevi.

   Utilizza la libreria Adobe Primetime authentication Media Token Verifier per verificare il token multimediale di breve durata restituito dal `getAuthorization()` chiama qui sopra:

   - Se la convalida ha esito positivo: Riprodurre il supporto richiesto per l&#39;utente.
   - Se la convalida non riesce: Il token AuthZ non è valido. La richiesta multimediale deve essere rifiutata e deve essere visualizzato un messaggio di errore all&#39;utente.

1. Torna al normale flusso di applicazioni.

### E. Visualizza flusso multimediale {#media_flow}

1. L&#39;utente seleziona il supporto da visualizzare.
1.  I media sono protetti?  L&#39;applicazione controlla se il supporto selezionato è protetto:
   - Se il supporto selezionato è protetto, l&#39;applicazione avvia la [Flusso di autorizzazione](#authz_flow) sopra.
   - Se il supporto selezionato non è protetto, riprodurlo per l&#39;utente.

### F. Flusso di disconnessione {#logout_flow}

1. Chiamata [`logout()`](#$logout) per disconnettersi dall&#39;utente. \
   AccessEnabler cancella tutti i valori e i token memorizzati nella cache ottenuti dall&#39;utente per l&#39;MVPD corrente su tutti i richiedenti che condividono l&#39;accesso tramite Single Sign-On. Dopo aver cancellato la cache, AccessEnabler effettua una chiamata al server per pulire le sessioni lato server.  Tieni presente che, poiché la chiamata al server potrebbe causare un reindirizzamento SAML all’IdP (questo consente la pulizia della sessione sul lato IdP), questa chiamata deve seguire tutti i reindirizzamenti. Per questo motivo, questa chiamata verrà gestita all&#39;interno di un controllo WebView, invisibile per l&#39;utente.

   **Nota:** Il flusso di logout è diverso dal flusso di autenticazione in quanto l&#39;utente non è tenuto a interagire in alcun modo con WebView. Pertanto è possibile (e consigliato) rendere invisibile il controllo WebView (ovvero: nascosto) durante il processo di logout.

