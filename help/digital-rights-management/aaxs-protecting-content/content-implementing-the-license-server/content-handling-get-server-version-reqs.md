---
seo-title: Gestione delle richieste Get Server Version
title: Gestione delle richieste Get Server Version
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestione delle richieste Get Server Version{#handling-get-server-version-requests}

Adobe Access client 3.0 e versioni successive inviano una richiesta Get Server Version per determinare le funzionalità del server. Tutti i server che utilizzano Adobe Access SDK 3.0 e versioni successive devono implementare il supporto per le richieste Get Server Version.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* L’URL della richiesta deve essere &quot;URL del server delle licenze nei metadati&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Per Adobe Access SDK 4.0 e versioni successive, la risposta a una richiesta Get Server Version indica ai client che il server supporta le versioni 3 e 4 del protocollo Adobe Access.
