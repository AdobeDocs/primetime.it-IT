---
seo-title: Gestione delle richieste di autenticazione
title: Gestione delle richieste di autenticazione
uuid: abcb9cf6-668e-405c-9659-9ed1bcc33024
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestione delle richieste di autenticazione {#handle-authentication-requests}

La `AuthenticationHandler` classe viene utilizzata per elaborare le richieste di autenticazione. Viene utilizzato solo per l’autenticazione tramite nome utente e password.

Durante la generazione del token di autenticazione, è necessario specificare la data di scadenza del token. Le proprietà personalizzate possono essere incluse anche nel token. Se impostata, tali proprietà saranno visibili al server quando il token di autenticazione viene inviato nelle richieste successive. Consulta [Gestione delle richieste](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) di licenza per informazioni sulla gestione dei token di autenticazione personalizzati.

Il gestore legge una richiesta di autenticazione e analizza il messaggio della richiesta quando `parseRequest()` viene chiamato. L&#39;implementazione del server esamina le credenziali utente nella richiesta e, se le credenziali sono valide, genera un `AuthenticationToken` oggetto chiamando `getRequest().generateAuthToken()`. Se non `AuthenticationRequestMessage.generateAuthToken()` viene chiamato prima `close()`, viene inviato un codice di errore di autenticazione.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL server licenze nei metadati: + &quot; [!DNL /flashaccess/authn/v4]&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client Adobe Primetime DRM ottengono quindi le richieste di autenticazione &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;

