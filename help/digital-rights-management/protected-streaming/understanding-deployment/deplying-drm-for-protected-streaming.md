---
title: Distribuzione del server Adobe Primetime DRM per lo streaming protetto
description: Distribuzione del server Adobe Primetime DRM per lo streaming protetto
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
