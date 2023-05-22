---
title: Gestione delle richieste di recupero versione del server
description: Gestione delle richieste di recupero versione del server
copied-description: true
exl-id: 125b0111-17e9-4f6f-954b-6975048cd2fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
