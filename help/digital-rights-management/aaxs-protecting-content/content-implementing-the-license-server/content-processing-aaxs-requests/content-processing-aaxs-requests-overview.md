---
seo-title: Panoramica
title: Panoramica
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Panoramica{#overview}

L&#39;approccio generale alla gestione delle richieste consiste nel creare un gestore, analizzare la richiesta, impostare i dati della risposta o il codice di errore e chiudere il gestore.

La classe di base utilizzata per gestire l&#39;interazione singola richiesta/risposta è `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Per inizializzare il gestore viene utilizzata un&#39;istanza della `HandlerConfiguration` classe. `HandlerConfiguration` memorizza le informazioni di configurazione del server, incluse le credenziali di trasporto, la tolleranza delle marche temporali, gli elenchi degli aggiornamenti dei criteri e gli elenchi delle revoche. Il gestore legge i dati della richiesta e analizza la richiesta in un&#39;istanza di `RequestMessageBase`. Il chiamante può esaminare le informazioni contenute nella richiesta e decidere se restituire un errore o una risposta corretta (le sottoclassi di `RequestMessageBase` forniscono un metodo per l&#39;impostazione dei dati di risposta).

Se la richiesta ha esito positivo, impostate i dati della risposta; altrimenti invocare `RequestMessageBase.setErrorData()` in caso di errore. Termina sempre l&#39;implementazione richiamando il `close()` metodo (si consiglia di `close()` chiamarlo nel `finally` blocco di un&#39; `try` istruzione). Per un esempio di come richiamare il gestore, consultate la documentazione di riferimento `MessageHandlerBase` API.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Il codice di stato HTTP 200 (OK) deve essere inviato in risposta a tutte le richieste elaborate dal gestore. Se non è stato possibile creare il gestore a causa di un errore del server, il server potrebbe rispondere con un altro codice di stato, ad esempio 500 (Errore interno del server).

Il client utilizza l&#39;URL del server licenze specificato al momento della creazione del pacchetto come URL di base per tutte le richieste inviate al server licenze. Ad esempio, se l’URL del server è specificato come &quot;<span></span>https://licenseserver.com/path&quot;, il client invierà le richieste a &quot;<span></span>https://licenseserver.com/path/flashaccess/...&quot;. Per informazioni dettagliate sul percorso specifico utilizzato per ciascun tipo di richiesta, consultate le sezioni seguenti. Quando implementate il server licenze, accertatevi che il server risponda ai percorsi richiesti per ciascun tipo di richiesta.

Una richiesta di licenza può contenere un token di autenticazione. Se è stata utilizzata l&#39;autenticazione tramite nome utente/password, la richiesta potrebbe contenere un `AuthenticationToken` elemento generato dal `AuthenticationHandler`, e l&#39;SDK verificherà che il token sia valido prima di rilasciare una licenza.
