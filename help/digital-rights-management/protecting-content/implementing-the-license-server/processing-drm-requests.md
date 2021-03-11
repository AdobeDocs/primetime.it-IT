---
title: Elabora richieste Adobe Primetime DRM
description: Elabora richieste Adobe Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# Elabora richieste Adobe Primetime DRM {#process-adobe-primetime-drm-requests}

L&#39;approccio generale alla gestione delle richieste consiste nel creare un gestore, analizzare la richiesta, impostare i dati di risposta o il codice di errore e chiudere il gestore.

La classe base utilizzata per gestire l&#39;interazione singola richiesta/risposta è `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Per inizializzare il gestore viene utilizzata un&#39;istanza della classe `HandlerConfiguration` . `HandlerConfiguration` memorizza le informazioni di configurazione del server, incluse le credenziali di trasporto, la tolleranza del timestamp, gli elenchi di aggiornamento dei criteri e gli elenchi di revoche. Il gestore legge i dati della richiesta e analizza la richiesta in un&#39;istanza di  `RequestMessageBase`. Il chiamante può esaminare le informazioni contenute nella richiesta e decidere se restituire un errore o una risposta corretta (le sottoclassi di `RequestMessageBase` forniscono un metodo per impostare i dati di risposta).

Se la richiesta ha esito positivo, imposta i dati di risposta; altrimenti richiama `RequestMessageBase.setErrorData()` in caso di errore. Termina sempre l&#39;implementazione richiamando il metodo `close()` (si consiglia di chiamare `close()` nel blocco `finally` di un&#39;istruzione `try`). Per un esempio su come richiamare il gestore, consulta la documentazione di riferimento API `MessageHandlerBase` .

>[!NOTE]
>
>Il codice di stato HTTP 200 (OK) deve essere inviato in risposta a tutte le richieste elaborate dal gestore. Se non è stato possibile creare il gestore a causa di un errore del server, il server potrebbe rispondere con un altro codice di stato, ad esempio 500 (Errore interno del server).

Il client utilizza l’URL del server licenze specificato al momento della creazione del pacchetto come URL di base per tutte le richieste inviate al server licenze. Ad esempio, se l&#39;URL del server è specificato come &lt;[!DNL ht<span></span>tps://licenseserver.com/path]>, il client invia quindi le richieste a &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/..]> Per informazioni dettagliate sul percorso specifico utilizzato per ciascun tipo di richiesta, consulta le sezioni seguenti. Quando implementi il server licenze, assicurati che il server risponda ai percorsi richiesti per ogni tipo di richiesta.

Una richiesta di licenza può contenere un token di autenticazione. Se è stata utilizzata l’autenticazione con nome utente/password, la richiesta può contenere un `AuthenticationToken` generato da `AuthenticationHandler` e l’SDK verificherà che il token sia valido prima di rilasciare una licenza.

## Utilizzare gli identificatori macchina {#use-machine-identifiers}

Tutte le richieste Adobe Primetime DRM (ad eccezione delle richieste che supportano la compatibilità FMRMS) includono informazioni sul token computer che è stato rilasciato al client durante l’individualizzazione. Il token del computer include un ID computer, che è un identificatore assegnato durante l&#39;individualizzazione. È possibile utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o è entrato in un dominio.

È possibile utilizzare un identificatore come segue:

* Il metodo `getUniqueId()` restituisce una stringa che è stata assegnata a un dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambia se l&#39;utente riformatta il disco rigido e si individualizza di nuovo. Questo identificatore ha anche un valore diverso tra Adobe AIR e Adobe Flash Player in diversi browser sullo stesso computer.
* Se si desidera contare più accuratamente le macchine, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è stato visto in precedenza, ottieni tutti gli identificatori per un nome utente e chiama `matches()` per verificare se esiste una corrispondenza. Poiché il metodo `matches()` deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è pratica solo quando vi sono pochi valori da confrontare; ad esempio, i computer associati a un utente specifico.

## Autenticazione utente {#user-authentication}

Una richiesta DRM di Adobe Primetime può contenere un token di autenticazione.

Se è stata utilizzata l&#39;autenticazione con nome utente/password, la richiesta può includere un `AuthenticationToken` generato da `AuthenticationHandler`. Per accedere al token e verificarlo, utilizza `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizza l’ `DRMManager.authenticate()` API ActionScript o iOS.

Se il client e il server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato utilizzando l’API `DRMManager.setAuthenticationToken` ActionScript 3.0. Utilizza `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L’implementazione del server determina se il token di autenticazione personalizzato è valido.

## Protezione di riproduzione {#replay-protection}

Per la protezione di ripetizione, potrebbe essere utile verificare se l&#39;identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, l&#39;autore dell&#39;attacco potrebbe tentare di riprodurre nuovamente la richiesta, che dovrebbe essere negata. Per rilevare i tentativi di ripetizione, il server può memorizzare un elenco di ID messaggio visualizzati di recente e controllare ogni richiesta in arrivo rispetto all’elenco memorizzato nella cache. Per limitare il tempo necessario alla memorizzazione degli identificatori del messaggio, invoca `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l&#39;SDK nega qualsiasi richiesta che trasporta una marca temporale per più di un numero specificato di secondi dall&#39;ora del server.

## Rilevamento di ripristino {#rollback-detection}

Per il rilevamento del rollback, alcune regole di utilizzo richiedono al client di mantenere le informazioni di stato per l&#39;applicazione dei diritti. Ad esempio, per applicare la regola di utilizzo della finestra di riproduzione, il client memorizza la data e l’ora in cui l’utente ha iniziato a visualizzare il contenuto per la prima volta. Questo evento attiva l&#39;avvio della finestra di riproduzione. Per applicare in modo sicuro la finestra di riproduzione, il server deve assicurarsi che l&#39;utente non esegua il backup e il ripristino dello stato del client per rimuovere l&#39;ora di avvio della finestra di riproduzione memorizzata sul client. Il server esegue questa operazione monitorando il valore del contatore di rollback del client.

Per ogni richiesta, il server ottiene il valore del contatore chiamando `RequestMessageBase.getClientState()` per ottenere l&#39;oggetto `ClientState`, quindi chiamando `ClientState.getCounter()` per ottenere il valore corrente del contatore dello stato client. Il server deve memorizzare questo valore per ogni client (utilizzare `MachineId.getUniqueId()` per identificare il client associato al valore del contatore di rollback), quindi chiamare `ClientState.incrementCounter()` per aumentare il valore del contatore di uno. Se il server rileva che il valore del contatore è inferiore all&#39;ultimo valore rilevato dal server, è possibile che sia stato eseguito il rollback dello stato client.

Per ulteriori informazioni sul rilevamento di manomissioni dello stato client, consulta la documentazione di riferimento API `ClientState` .

## Dati di configurazione del server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare il modo in cui vengono applicate le licenze. Questo viene fatto creando una classe `ServerConfigData` e chiamando `HandlerConfiguration.setServerConfigData()`. Queste impostazioni si applicano solo alle licenze rilasciate dal server licenze.

La tolleranza del tempo indesiderato è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il cliente applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio della macchina indietro di 4 ore senza invalidare le licenze. Se un operatore del server di licenza desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nella classe `ServerConfigData` . Quando modifichi il valore di una di queste impostazioni, assicurati di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori vengono inviati al client solo se la versione sul client è precedente alla versione corrente `ServerConfigData`.

## File dei criteri DRM tra domini diversi {#crossdomain-drm-policy-file}

Se il server licenze è ospitato su un dominio diverso dal file SWF di riproduzione video, è necessario un file di criteri DRM tra più domini ( [!DNL crossdomain.xml]) per consentire al file SWF di richiedere licenze da un server licenze. Un file di criteri DRM tra più domini è rappresentato da un file XML che consente al server di indicare che i suoi dati e documenti sono disponibili per i file SWF provenienti da altri domini. A qualsiasi file SWF gestito da un dominio specificato nel file di criteri DRM tra domini del server licenze è consentito accedere ai dati o alle risorse da tale server licenze.

L’Adobe consiglia agli sviluppatori di seguire le best practice durante la distribuzione del file dei criteri tra domini diversi, consentendo solo ai domini affidabili di accedere al server licenze e limitando l’accesso alla sottodirectory delle licenze sul server web.

Per ulteriori informazioni sui file di criteri DRM tra più domini, consulta le seguenti posizioni:

* Controlli del sito web (file di criteri DRM)
* Specifica del file dei criteri DRM tra domini diversi: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)