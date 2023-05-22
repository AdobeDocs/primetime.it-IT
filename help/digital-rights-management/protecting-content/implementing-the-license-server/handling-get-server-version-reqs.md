---
title: Gestire le richieste di recupero versione del server
description: Gestire le richieste di recupero versione del server
copied-description: true
exl-id: 86a1bbe3-2ae4-4d4e-be51-fbbeb32147c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Gestire le richieste di recupero versione del server {#handle-get-server-version-requests}

Il client Adobe Primetime DRM 3.0 o versione successiva invia una richiesta Get Server Version per determinare le funzionalità del server. Tutti i server che utilizzano Primetime DRM SDK 3.0 o versione successiva devono implementare il supporto per le richieste Get Server Version.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* L’URL della richiesta deve essere &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Per Primetime DRM SDK 4.0 o versione successiva, la risposta a una richiesta Get Server Version indica ai client che il server supporta le versioni 3 e 4 del protocollo DRM di Primetime.
