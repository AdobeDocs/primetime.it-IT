---
seo-title: Gestione delle richieste di versione del server Get
title: Gestione delle richieste di versione del server Get
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Gestire le richieste di recupero versione server {#handle-get-server-version-requests}

 Adobe Primetime DRM client 3.0 o versione successiva invia una richiesta Get Server Version per determinare le funzionalità del server. Tutti i server che utilizzano Primetime DRM SDK 3.0 o versione successiva devono implementare il supporto per le richieste Get Server Version.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* L&#39;URL della richiesta deve essere &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Per Primetime DRM SDK 4.0 o versione successiva, la risposta a una richiesta Get Server Version indica ai client che il server supporta le versioni 3 e 4 del protocollo Primetime DRM.
