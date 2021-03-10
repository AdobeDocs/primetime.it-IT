---
title: Gestire le richieste di autenticazione
description: Gestire le richieste di autenticazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Gestire le richieste di autenticazione {#handle-authentication-requests}

La classe `AuthenticationHandler` viene utilizzata per elaborare le richieste di autenticazione. Viene utilizzato solo per l’autenticazione con nome utente e password.

Quando si genera il token di autenticazione, è necessario specificare la data di scadenza del token. Nel token possono essere incluse anche le proprietà personalizzate. Se impostate, queste proprietà saranno visibili al server quando il token di autenticazione viene inviato nelle richieste successive. Per informazioni sulla gestione dei token di autenticazione personalizzati, consulta [Gestione delle richieste di licenza](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) .

Il gestore legge una richiesta di autenticazione e analizza il messaggio di richiesta quando viene chiamato `parseRequest()`. L&#39;implementazione del server esamina le credenziali utente nella richiesta e, se le credenziali sono valide, genera un oggetto `AuthenticationToken` chiamando `getRequest().generateAuthToken()`. Se `AuthenticationRequestMessage.generateAuthToken()` non viene chiamato prima di `close()`, viene inviato un codice di errore di autenticazione.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* Se il protocollo di supporto client e server versione 5, l’URL della richiesta è &quot;URL del server licenze nei metadati: + &quot; [!DNL /flashaccess/authn/v4]&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client Adobe Primetime DRM inoltrano le richieste di autenticazione a &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/authn/v3]&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/authn/v1]&quot;

