---
title: Panoramica
description: Panoramica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Panoramica{#overview}

L’approccio generale alla gestione delle richieste consiste nel creare un gestore, analizzare la richiesta, impostare i dati di risposta o il codice di errore e chiudere il gestore.

La classe base utilizzata per gestire una singola interazione richiesta/risposta è `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Un&#39;istanza di `HandlerConfiguration` viene utilizzata per inizializzare il gestore. `HandlerConfiguration` memorizza le informazioni di configurazione del server, incluse le credenziali di trasporto, la tolleranza di marca temporale, gli elenchi di aggiornamento dei criteri e gli elenchi di revoca. Il gestore legge i dati della richiesta e analizza la richiesta in un&#39;istanza di `RequestMessageBase`. Il chiamante può esaminare le informazioni nella richiesta e decidere se restituire un errore o una risposta corretta (sottoclassi di `RequestMessageBase` fornisce un metodo per impostare i dati di risposta).

Se la richiesta ha esito positivo, imposta i dati di risposta; in caso contrario, richiama `RequestMessageBase.setErrorData()` in caso di guasto. Termina sempre l’implementazione richiamando `close()` metodo (si consiglia di `close()` essere richiamato in `finally` blocco di un `try` istruzione ). Consulta la `MessageHandlerBase` Documentazione di riferimento API per un esempio di come richiamare il gestore.

>[!NOTE]
>
>Il codice di stato HTTP 200 (OK) deve essere inviato in risposta a tutte le richieste elaborate dal gestore. Se non è stato possibile creare il gestore a causa di un errore del server, il server potrebbe rispondere con un altro codice di stato, ad esempio 500 (Errore interno del server).

Il client utilizza l&#39;URL del server licenze specificato al momento del packaging come URL di base per tutte le richieste inviate al server licenze. Ad esempio, se l’URL del server è specificato come &quot;ht<span></span>tps://licenseserver.com/path&quot;, il client invierà le richieste a &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;. Per informazioni dettagliate sul percorso specifico utilizzato per ciascun tipo di richiesta, consulta le sezioni seguenti. Quando implementi il server licenze, accertati che risponda ai percorsi richiesti per ogni tipo di richiesta.

Una richiesta di licenza può contenere un token di autenticazione. Se è stata utilizzata l’autenticazione nome utente/password, la richiesta può contenere `AuthenticationToken` generato da `AuthenticationHandler`e l’SDK garantirà la validità del token prima di rilasciare una licenza.
