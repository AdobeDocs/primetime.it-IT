---
title: Gestione delle richieste di autenticazione
description: Gestione delle richieste di autenticazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Gestione delle richieste di autenticazione{#handling-authentication-requests}

Il `AuthenticationHandler` La classe viene utilizzata per elaborare le richieste di autenticazione. Viene utilizzato solo per l’autenticazione nome utente/password.

Durante la generazione del token di autenticazione, è necessario specificare la data di scadenza del token. Nel token possono essere incluse anche le proprietà personalizzate. Se impostate, queste proprietà saranno visibili al server quando il token di autenticazione viene inviato nelle richieste successive. Consulta [Gestione delle richieste di licenza](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) per informazioni sulla gestione dei token di autenticazione personalizzati.

Il gestore legge una richiesta di autenticazione e analizza il messaggio di richiesta quando `parseRequest()` viene chiamato. L’implementazione del server esamina le credenziali utente nella richiesta e, se le credenziali sono valide, genera un’ `AuthenticationToken` oggetto chiamando `getRequest().generateAuthToken()`. Se `AuthenticationRequestMessage.generateAuthToken()` non è chiamato prima di `close()`, viene inviato un codice di errore di autenticazione.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Se sia il client che il server supportano la versione 5 del protocollo, l&#39;URL della richiesta è &quot;License Server URL in metadata: + &quot;/flashaccess/authn/v4&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client Adobe Access invieranno richieste di autenticazione a &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/authn/v3&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/authn/v1&quot;
