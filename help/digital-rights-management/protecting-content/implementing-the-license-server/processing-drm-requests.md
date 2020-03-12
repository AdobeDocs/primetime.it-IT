---
seo-title: Elabora richieste DRM Adobe Primetime
title: Elabora richieste DRM Adobe Primetime
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Elabora richieste DRM Adobe Primetime {#process-adobe-primetime-drm-requests}

L&#39;approccio generale alla gestione delle richieste consiste nel creare un gestore, analizzare la richiesta, impostare i dati o il codice di errore della risposta e chiudere il gestore.

La classe di base utilizzata per gestire l&#39;interazione singola richiesta/risposta è `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Per inizializzare il gestore viene utilizzata un&#39;istanza della `HandlerConfiguration` classe. `HandlerConfiguration` memorizza le informazioni di configurazione del server, incluse le credenziali di trasporto, la tolleranza delle marche temporali, gli elenchi degli aggiornamenti dei criteri e gli elenchi delle revoche. Il gestore legge i dati della richiesta e analizza la richiesta in un&#39;istanza di `RequestMessageBase`. Il chiamante può esaminare le informazioni contenute nella richiesta e decidere se restituire un errore o una risposta corretta (le sottoclassi di `RequestMessageBase` forniscono un metodo per l&#39;impostazione dei dati di risposta).

Se la richiesta ha esito positivo, impostate i dati della risposta; altrimenti invocare `RequestMessageBase.setErrorData()` in caso di errore. Termina sempre l&#39;implementazione richiamando il `close()` metodo (si consiglia di `close()` chiamarlo nel `finally` blocco di un&#39; `try` istruzione). Per un esempio di come richiamare il gestore, consultate la documentazione di riferimento `MessageHandlerBase` API.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Il codice di stato HTTP 200 (OK) deve essere inviato in risposta a tutte le richieste elaborate dal gestore. Se non è stato possibile creare il gestore a causa di un errore del server, il server potrebbe rispondere con un altro codice di stato, ad esempio 500 (Errore interno del server).

Il client utilizza l&#39;URL del server licenze specificato al momento della creazione del pacchetto come URL di base per tutte le richieste inviate al server licenze. Ad esempio, se l&#39;URL del server è specificato come &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, il client invia quindi le richieste a &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> Per informazioni dettagliate sul percorso specifico utilizzato per ciascun tipo di richiesta, vedere le sezioni seguenti. Quando implementate il server licenze, accertatevi che il server risponda ai percorsi richiesti per ciascun tipo di richiesta.

Una richiesta di licenza può contenere un token di autenticazione. Se è stata utilizzata l&#39;autenticazione tramite nome utente/password, la richiesta potrebbe contenere un `AuthenticationToken` elemento generato dal `AuthenticationHandler`, e l&#39;SDK verificherà che il token sia valido prima di rilasciare una licenza.

## Utilizzare gli identificatori del computer {#use-machine-identifiers}

Tutte le richieste DRM di Adobe Primetime (ad eccezione delle richieste che supportano la compatibilità FMRMS) includono informazioni sul token computer che è stato rilasciato al client durante l&#39;individualizzazione. Il token del computer include un ID computer, che è un identificatore assegnato durante l&#39;individualizzazione. Potete utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o ha aderito a un dominio.

Potete usare un identificatore come segue:

* Il `getUniqueId()` metodo restituisce una stringa che è stata assegnata a un dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore viene modificato se l&#39;utente riformatta il disco rigido e lo individua di nuovo. Questo identificatore ha anche un valore diverso tra Adobe AIR e Adobe Flash Player in diversi browser sullo stesso computer.
* Se si desidera contare più accuratamente i computer, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è stato visto in precedenza, ottenere tutti gli identificatori per un nome utente e chiamare `matches()` per verificare se esiste una corrispondenza. Poiché il `matches()` metodo deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è pratica solo se vi è un numero limitato di valori da confrontare; ad esempio, i computer associati a un utente specifico.

## Autenticazione utente {#user-authentication}

Una richiesta Adobe Primetime DRM può contenere un token di autenticazione.

Se è stata utilizzata l&#39;autenticazione tramite nome utente/password, la richiesta potrebbe includere un `AuthenticationToken` generato dal `AuthenticationHandler`. Per accedere e verificare il token, è necessario utilizzare `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizzate l&#39;API `DRMManager.authenticate()` ActionScript o iOS.

Se client e server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato tramite l&#39;API `DRMManager.setAuthenticationToken` ActionScript 3.0. Utilizzare `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L&#39;implementazione del server determina se il token di autenticazione personalizzato è valido.

## Protezione di ripetizione {#replay-protection}

Per la protezione di ripetizione, potrebbe essere utile verificare se l&#39;identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, un utente malintenzionato potrebbe tentare di riprodurre nuovamente la richiesta, cosa che dovrebbe essere negata. Per rilevare i tentativi di riproduzione, il server può memorizzare un elenco di ID messaggio visti di recente e controllare ogni richiesta in entrata rispetto all&#39;elenco memorizzato nella cache. Per limitare il tempo necessario per memorizzare gli identificatori del messaggio, chiama `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l’SDK nega quindi qualsiasi richiesta con marca temporale per più di un numero specificato di secondi dall’ora del server.

## Rilevamento del rollback {#rollback-detection}

Per il rilevamento del rollback, alcune regole di utilizzo richiedono al client di mantenere le informazioni di stato per l&#39;applicazione dei diritti. Ad esempio, per applicare la regola di utilizzo della finestra di riproduzione, il client memorizza la data e l&#39;ora in cui l&#39;utente ha iniziato a visualizzare il contenuto per la prima volta. Questo evento attiva l&#39;avvio della finestra di riproduzione. Per applicare in modo sicuro la finestra di riproduzione, il server deve assicurarsi che l&#39;utente non effettui il backup e ripristini lo stato del client per rimuovere l&#39;ora di inizio della finestra di riproduzione memorizzata sul client. Il server esegue questa operazione monitorando il valore del contatore di rollback del client.

Per ogni richiesta, il server ottiene il valore del contatore chiamando `RequestMessageBase.getClientState()` per ottenere l&#39; `ClientState` oggetto, quindi chiamando `ClientState.getCounter()` per ottenere il valore corrente del contatore dello stato del client. Il server deve memorizzare questo valore per ciascun client (utilizzare `MachineId.getUniqueId()` per identificare il client associato al valore del contatore di rollback), quindi chiamare `ClientState.incrementCounter()` per aumentare il valore del contatore di uno. Se il server rileva che il valore del contatore è inferiore all&#39;ultimo valore visualizzato dal server, è possibile che sia stato eseguito il rollback dello stato del client.

Per ulteriori informazioni sul rilevamento di eventuali manomissioni da parte del cliente, consultate la documentazione di riferimento `ClientState` API.

## Dati di configurazione del server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare come vengono applicate le licenze. Questa operazione viene eseguita creando una `ServerConfigData` classe e chiamando `HandlerConfiguration.setServerConfigData()`. Queste impostazioni si applicano solo alle licenze rilasciate da questo server licenze.

La tolleranza per il windback dell&#39;orologio è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il client applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio del computer indietro di 4 ore senza invalidare le licenze. Se un operatore del server licenze desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nella `ServerConfigData` classe. Quando modificate il valore di una di queste impostazioni, accertatevi di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori vengono inviati al client solo se la versione sul client è precedente alla `ServerConfigData` versione corrente.

## File criteri DRM tra domini {#crossdomain-drm-policy-file}

Se il server licenze è ospitato su un dominio diverso dal file SWF di riproduzione video, è necessario un file di criteri DRM ( [!DNL crossdomain.xml]) tra più domini per consentire al file SWF di richiedere licenze da un server licenze. Un file di criteri DRM tra domini è rappresentato da un file XML che consente al server di indicare che i suoi dati e documenti sono disponibili per i file SWF gestiti da altri domini. Tutti i file SWF gestiti da un dominio specificato nel file di criteri DRM del server licenze possono accedere ai dati o alle risorse da tale server licenze.

Adobe consiglia agli sviluppatori di seguire le procedure ottimali durante la distribuzione del file dei criteri per i domini diversi, consentendo solo ai domini trusted di accedere al server delle licenze e limitando l&#39;accesso alla sottodirectory delle licenze sul server Web.

Per ulteriori informazioni sui file di criteri DRM tra domini, consulta le seguenti posizioni:

* Controlli del sito Web (file di criteri DRM)
* Specifica del file del criterio DRM tra domini: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)