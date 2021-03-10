---
title: Gestione delle richieste Get Server Version
description: Gestione delle richieste Get Server Version
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Gestione delle richieste Get Server Version{#handling-get-server-version-requests}

Adobe Access client 3.0 e versioni successive inviano una richiesta Get Server Version per determinare le funzionalità del server. Tutti i server che utilizzano Adobe Access SDK 3.0 e versioni successive devono implementare il supporto per le richieste Get Server Version.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* L&#39;URL della richiesta deve essere &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Ad Adobe Access SDK 4.0 e versioni successive, la risposta a una richiesta Get Server Version indica ai client che il server supporta le versioni 3 e 4 del protocollo Adobe Access.
