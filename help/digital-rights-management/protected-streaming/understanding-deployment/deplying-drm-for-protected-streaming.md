---
seo-title: Implementazione di  Adobe Primetime DRM Server per lo streaming protetto
title: Implementazione di  Adobe Primetime DRM Server per lo streaming protetto
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Implementazione di  Adobe Primetime DRM Server per lo streaming protetto{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Per poter distribuire  Adobe Primetime DRM Server for Protected Streaming, è necessario aver installato le versioni di Java e Tomcat elencate nell&#39;argomento Requisiti.

Il pacchetto Primetime DRM Server for Protected Streaming include [!DNL flashaccesserver.war]. Se:

* Per distribuire questo file WAR, è necessario copiarlo nella [!DNL webapps] directory di Tomcat.
* Hai già distribuito il file WAR, potrebbe essere necessario eliminare la directory WAR non imballato ( [!DNL flashaccessserver] nella directory di Tomcat [!DNL webapps] ).

* Vuoi impedire a Tomcat di disfare i file WAR, modificare il [!DNL server.xml] file nella [!DNL conf] directory di Tomcat e configurare l&#39; `unpackWARs` attributo iby impostandolo su `false`.

>[!NOTE]
>
>Se avete configurato Tomcat per l&#39;inclusione [!DNL commons-logging.jar] nel percorso di classe di sistema (non richiesto per il server DRM di Primetime per lo streaming protetto), dovete configurare la registrazione dei commons per l&#39;utilizzo di Log4J.

Il server utilizza facoltativamente una libreria specifica per la piattaforma ( [!DNL jsafe.dll] in Microsoft Windows o [!DNL libjsafe.so] in Linux) per ottenere prestazioni ottimali. Potete copiare la libreria appropriata per la piattaforma dalla [!DNL thirdparty/cryptoj/]*piattaforma *a una posizione specificata dalla variabile di`PATH`ambiente o`LD_LIBRARY_PATH`su Linux.

>[!NOTE]
>
>È consigliabile utilizzare la versione a 64 bit solo se il sistema operativo e il JDK supportano la versione a 64 bit. In caso contrario, è necessario utilizzare la versione a 32 bit.

