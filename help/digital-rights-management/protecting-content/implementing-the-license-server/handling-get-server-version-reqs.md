---
title: Gestire le richieste di versione del server Get
description: Gestire le richieste di versione del server Get
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Gestire le richieste Get Server Version {#handle-get-server-version-requests}

Adobe Primetime DRM client 3.0 o versione successiva invia una richiesta Get Server Version per determinare le funzionalità del server. Tutti i server che utilizzano Primetime DRM SDK 3.0 o successivo devono implementare il supporto per le richieste Get Server Version.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* L&#39;URL della richiesta deve essere &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Per Primetime DRM SDK 4.0 o successivo, la risposta a una richiesta Get Server Version indica ai client che il server supporta le versioni 3 e 4 del protocollo Primetime DRM.
