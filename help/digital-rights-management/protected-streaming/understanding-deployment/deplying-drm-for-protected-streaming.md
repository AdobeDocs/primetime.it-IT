---
title: Distribuzione del server Adobe Primetime DRM per lo streaming protetto
description: Distribuzione del server Adobe Primetime DRM per lo streaming protetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Distribuzione del server Adobe Primetime DRM per lo streaming protetto{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Prima di distribuire Adobe Primetime DRM Server for Protected Streaming, è necessario aver installato le versioni di Java e Tomcat elencate nell&#39;argomento Requisiti.

Il pacchetto Primetime DRM Server for Protected Streaming include [!DNL flashaccesserver.war]. Se:

* Se desideri distribuire questo file WAR, devi copiarlo nel file Tomcat di [!DNL webapps] directory.
* Se in precedenza è stato distribuito il file WAR, potrebbe essere necessario eliminare la directory WAR decompressa ( [!DNL flashaccessserver] in Tomcat [!DNL webapps] directory).

* Per impedire a Tomcat di decomprimere i file WAR, modificare la [!DNL server.xml] file in Tomcat [!DNL conf] e configurare il `unpackWARs` attributo impostandolo su `false`.

>[!NOTE]
>
>Se hai configurato Tomcat per includere [!DNL commons-logging.jar] in System classpath (non richiesto per Primetime DRM Server for Protected Streaming) è necessario configurare commons-logging per utilizzare Log4J.

Il server utilizza facoltativamente una libreria specifica della piattaforma ( [!DNL jsafe.dll] in Microsoft Windows o [!DNL libjsafe.so] su Linux per prestazioni ottimali. Puoi copiare la libreria appropriata per la tua piattaforma da [!DNL thirdparty/cryptoj/]*piattaforma* in una posizione specificata da `PATH` variabile di ambiente o `LD_LIBRARY_PATH` su Linux.

>[!NOTE]
>
>È consigliabile utilizzare la versione a 64 bit solo se il sistema operativo e il JDK supportano entrambi i bit 64. In caso contrario, è necessario utilizzare la versione a 32 bit.
