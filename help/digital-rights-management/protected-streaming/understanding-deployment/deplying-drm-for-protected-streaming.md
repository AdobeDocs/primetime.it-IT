---
title: Distribuzione del server DRM di Adobe Primetime per lo streaming protetto
description: Distribuzione del server DRM di Adobe Primetime per lo streaming protetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Distribuzione del server DRM di Adobe Primetime per lo streaming protetto{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Prima di poter distribuire il server DRM di Adobe Primetime per lo streaming protetto, è necessario aver installato le versioni di Java e Tomcat elencate nell&#39;argomento Requisiti.

Il pacchetto Primetime DRM Server for Protected Streaming include [!DNL flashaccesserver.war]. Se:

* Per distribuire questo file WAR, è necessario copiarlo nella directory [!DNL webapps] di Tomcat.
* Dopo aver distribuito in precedenza il file WAR, potrebbe essere necessario eliminare la directory WAR decompressa ( [!DNL flashaccessserver] nella directory [!DNL webapps] di Tomcat).

* Per evitare che Tomcat scompili i file WAR, modifica il file [!DNL server.xml] nella directory [!DNL conf] di Tomcat e configura l&#39;impostazione dell&#39;attributo iby `unpackWARs` su `false`.

>[!NOTE]
>
>Se hai configurato Tomcat in modo da includere [!DNL commons-logging.jar] nel percorso di classe del sistema (non necessario per il server DRM di Primetime per lo streaming protetto), devi configurare la registrazione dei contenuti condivisi per utilizzare Log4J.

Il server utilizza facoltativamente una libreria specifica per la piattaforma ( [!DNL jsafe.dll] in Microsoft Windows o [!DNL libjsafe.so] su Linux per ottenere prestazioni ottimali. Puoi copiare la libreria appropriata per la piattaforma da [!DNL thirdparty/cryptoj/]*platform* in una posizione specificata dalla variabile di ambiente `PATH` o `LD_LIBRARY_PATH` su Linux.

>[!NOTE]
>
>Utilizzare la versione a 64 bit solo se sia il sistema operativo che JDK supportano 64 bit. In caso contrario, è necessario utilizzare la versione a 32 bit.

