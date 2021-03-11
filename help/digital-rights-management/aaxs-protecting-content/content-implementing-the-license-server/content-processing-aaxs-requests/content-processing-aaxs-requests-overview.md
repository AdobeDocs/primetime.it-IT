---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Panoramica{#overview}

L&#39;approccio generale alla gestione delle richieste consiste nel creare un gestore, analizzare la richiesta, impostare i dati di risposta o il codice di errore e chiudere il gestore.

La classe base utilizzata per gestire l&#39;interazione singola richiesta/risposta è `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Per inizializzare il gestore viene utilizzata un&#39;istanza della classe `HandlerConfiguration` . `HandlerConfiguration` memorizza le informazioni di configurazione del server, incluse le credenziali di trasporto, la tolleranza del timestamp, gli elenchi di aggiornamento dei criteri e gli elenchi di revoche. Il gestore legge i dati della richiesta e analizza la richiesta in un&#39;istanza di  `RequestMessageBase`. Il chiamante può esaminare le informazioni contenute nella richiesta e decidere se restituire un errore o una risposta corretta (le sottoclassi di `RequestMessageBase` forniscono un metodo per impostare i dati di risposta).

Se la richiesta ha esito positivo, imposta i dati di risposta; altrimenti richiama `RequestMessageBase.setErrorData()` in caso di errore. Termina sempre l&#39;implementazione richiamando il metodo `close()` (si consiglia di chiamare `close()` nel blocco `finally` di un&#39;istruzione `try`). Per un esempio su come richiamare il gestore, consulta la documentazione di riferimento API `MessageHandlerBase` .

>[!NOTE]
>
>Il codice di stato HTTP 200 (OK) deve essere inviato in risposta a tutte le richieste elaborate dal gestore. Se non è stato possibile creare il gestore a causa di un errore del server, il server potrebbe rispondere con un altro codice di stato, ad esempio 500 (Errore interno del server).

Il client utilizza l’URL del server licenze specificato al momento della creazione del pacchetto come URL di base per tutte le richieste inviate al server licenze. Ad esempio, se l’URL del server è specificato come &quot;ht<span></span>tps://licenseserver.com/path&quot;, il client invierà le richieste a &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/..&quot;. Consulta le sezioni seguenti per i dettagli sul percorso specifico utilizzato per ciascun tipo di richiesta. Quando implementi il server licenze, assicurati che il server risponda ai percorsi richiesti per ogni tipo di richiesta.

Una richiesta di licenza può contenere un token di autenticazione. Se è stata utilizzata l’autenticazione con nome utente/password, la richiesta può contenere un `AuthenticationToken` generato da `AuthenticationHandler` e l’SDK verificherà che il token sia valido prima di rilasciare una licenza.
