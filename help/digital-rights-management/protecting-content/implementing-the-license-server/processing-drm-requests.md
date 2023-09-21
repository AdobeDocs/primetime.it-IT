---
title: Elabora richieste Adobe Primetime DRM
description: Elabora richieste Adobe Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# Elabora richieste Adobe Primetime DRM {#process-adobe-primetime-drm-requests}

L’approccio generale alla gestione delle richieste consiste nel creare un gestore, analizzare la richiesta, impostare i dati di risposta o il codice di errore e chiudere il gestore.

La classe base utilizzata per gestire una singola interazione richiesta/risposta è `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Un&#39;istanza di `HandlerConfiguration` viene utilizzata per inizializzare il gestore. `HandlerConfiguration` memorizza le informazioni di configurazione del server, incluse le credenziali di trasporto, la tolleranza di marca temporale, gli elenchi di aggiornamento dei criteri e gli elenchi di revoca. Il gestore legge i dati della richiesta e analizza la richiesta in un&#39;istanza di `RequestMessageBase`. Il chiamante può esaminare le informazioni nella richiesta e decidere se restituire un errore o una risposta corretta (sottoclassi di `RequestMessageBase` fornisce un metodo per impostare i dati di risposta).

Se la richiesta ha esito positivo, imposta i dati di risposta; in caso contrario, richiama `RequestMessageBase.setErrorData()` in caso di guasto. Termina sempre l’implementazione richiamando `close()` metodo (si consiglia di `close()` essere richiamato in `finally` blocco di un `try` istruzione ). Consulta la `MessageHandlerBase` Documentazione di riferimento API per un esempio di come richiamare il gestore.

>[!NOTE]
>
>Il codice di stato HTTP 200 (OK) deve essere inviato in risposta a tutte le richieste elaborate dal gestore. Se non è stato possibile creare il gestore a causa di un errore del server, il server potrebbe rispondere con un altro codice di stato, ad esempio 500 (Errore interno del server).

Il client utilizza l&#39;URL del server licenze specificato al momento del packaging come URL di base per tutte le richieste inviate al server licenze. Ad esempio, se l&#39;URL del server è specificato come &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, il client invia quindi le richieste a &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/.]> Per informazioni dettagliate sul percorso specifico utilizzato per ciascun tipo di richiesta, consulta le sezioni seguenti. Quando implementi il server licenze, accertati che risponda ai percorsi richiesti per ogni tipo di richiesta.

Una richiesta di licenza può contenere un token di autenticazione. Se è stata utilizzata l’autenticazione nome utente/password, la richiesta può contenere `AuthenticationToken` generato da `AuthenticationHandler`e l’SDK garantirà la validità del token prima di rilasciare una licenza.

## Usa identificatori macchina {#use-machine-identifiers}

Tutte le richieste DRM di Adobe Primetime (ad eccezione delle richieste che supportano la compatibilità FMRMS) includono informazioni sul token del computer rilasciato al client durante l’individualizzazione. Il token del computer include un ID computer, che è un identificatore assegnato durante l’individualizzazione. È possibile utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o è entrato in un dominio.

Puoi utilizzare un identificatore come segue:

* Il `getUniqueId()` Il metodo restituisce una stringa assegnata a un dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambia se l&#39;utente riformatta il disco rigido e individualizza nuovamente. Questo identificatore ha anche un valore diverso tra Adobe AIR e il Flash Player Adobe in browser diversi sulla stessa macchina.
* Se si desidera contare con maggiore precisione i macchinari, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è già stato visto in precedenza, ottieni tutti gli identificatori per un nome utente e una chiamata `matches()` per verificare eventuali corrispondenze. Perché il `matches()` deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è utile solo quando è presente un numero limitato di valori da confrontare, ad esempio i computer associati a un utente specifico.

## Autenticazione utente {#user-authentication}

Una richiesta Adobe Primetime DRM può contenere un token di autenticazione.

Se è stata utilizzata l’autenticazione nome utente/password, la richiesta può includere `AuthenticationToken` generato da `AuthenticationHandler`. Se desideri accedere e verificare il token, devi utilizzare `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizzare `DRMManager.authenticate()` API ActionScript o iOS.

Se il client e il server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato utilizzando `DRMManager.setAuthenticationToken` API ActionScript 3.0. Utilizzare `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L’implementazione del server determina se il token di autenticazione personalizzato è valido.

## Protezione dalla ripetizione {#replay-protection}

Per la protezione dalla ripetizione, è possibile verificare se l’identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, l’autore dell’attacco potrebbe tentare di ripetere la richiesta, che dovrebbe essere negata. Per rilevare i tentativi di ripetizione, il server può memorizzare un elenco degli ID di messaggi visualizzati di recente e confrontare ogni richiesta in ingresso con l’elenco memorizzato nella cache. Per limitare il tempo di memorizzazione degli identificatori del messaggio, invoca `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l&#39;SDK nega quindi qualsiasi richiesta che presenti una marca temporale superiore al numero di secondi specificati fuori dall&#39;ora del server.

## Rilevamento rollback {#rollback-detection}

Per il rilevamento del rollback, alcune regole di utilizzo richiedono al client di mantenere le informazioni sullo stato per l&#39;applicazione dei diritti. Ad esempio, per applicare la regola di utilizzo della finestra di riproduzione, il client memorizza la data e l’ora in cui l’utente ha iniziato a visualizzare il contenuto per la prima volta. Questo evento attiva l’inizio della finestra di riproduzione. Per applicare in modo sicuro la finestra di riproduzione, il server deve assicurarsi che l&#39;utente non esegua il backup e ripristini lo stato del client per rimuovere l&#39;ora di inizio della finestra di riproduzione memorizzata sul client. Il server esegue questa operazione tenendo traccia del valore del contatore di rollback del client.

Per ogni richiesta, il server ottiene il valore del contatore chiamando `RequestMessageBase.getClientState()` per ottenere `ClientState` oggetto, quindi chiamata `ClientState.getCounter()` per ottenere il valore corrente del contatore stato client. Il server deve memorizzare questo valore per ogni client (utilizzare `MachineId.getUniqueId()` per identificare il client associato al valore del contatore di rollback), quindi chiamare `ClientState.incrementCounter()` per aumentare di uno il valore del contatore. Se il server rileva che il valore del contatore è minore dell&#39;ultimo valore visualizzato dal server, è possibile che sia stato eseguito il rollback dello stato del client.

Consulta la `ClientState` Documentazione di riferimento API per ulteriori informazioni sul rilevamento di manomissioni dello stato del client.

## Dati di configurazione server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare come vengono applicate le licenze. Ciò avviene tramite la creazione di un `ServerConfigData` classe e chiamata `HandlerConfiguration.setServerConfigData()`. Queste impostazioni si applicano solo alle licenze rilasciate da questo server licenze.

La tolleranza di clock windback è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il client applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio del computer indietro di 4 ore senza invalidare le licenze. Se un operatore del server licenze desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nel `ServerConfigData` classe. Quando modifichi il valore di una di queste impostazioni, accertati di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori vengono inviati al client solo se la versione del client è precedente a quella corrente `ServerConfigData` versione.

## File di criteri DRM tra domini {#crossdomain-drm-policy-file}

Se il server licenze è ospitato su un dominio diverso rispetto al SWF di riproduzione video, viene creato un file di criteri DRM tra domini diversi ( [!DNL crossdomain.xml]) è necessario per consentire al SWF di richiedere licenze da un server licenze. Un file di criteri DRM tra domini diversi è rappresentato da un file XML che consente al server di indicare che i relativi dati e documenti sono disponibili per i file SWF forniti da altri domini. Qualsiasi file SWF gestito da un dominio specificato nel file dei criteri DRM del server licenze tra domini diversi può accedere ai dati o alle risorse da tale server licenze.

L’Adobe consiglia agli sviluppatori di seguire le best practice durante la distribuzione del file di criteri tra domini diversi, consentendo solo ai domini trusted di accedere al server licenze e limitando l’accesso alla sottodirectory della licenza sul server web.

Per ulteriori informazioni sui file dei criteri DRM tra domini, vedere i percorsi seguenti:

* Controlli del sito Web (file di criteri DRM)
* Specifica del file di criteri DRM tra domini: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
