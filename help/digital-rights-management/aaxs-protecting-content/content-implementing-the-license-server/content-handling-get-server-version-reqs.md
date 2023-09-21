---
title: Gestione delle richieste di recupero versione del server
description: Gestione delle richieste di recupero versione del server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Gestione delle richieste di recupero versione del server{#handling-get-server-version-requests}

Adobe Access Client 3.0 e versioni successive inviano una richiesta di lettura della versione del server per determinare le funzionalità del server. Tutti i server che utilizzano Adobe Access SDK 3.0 e versioni successive devono implementare il supporto per le richieste di recupero della versione del server.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* L’URL della richiesta deve essere &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Ad Adobe, Access SDK 4.0 e versioni successive, la risposta a una richiesta Get Server Version indica ai client che il server supporta le versioni 3 e 4 del protocollo Adobe Access.
