---
title: Panoramica sulla distribuzione di Adobe Access Server for Protected Streaming
description: Panoramica sulla distribuzione di Adobe Access Server for Protected Streaming
copied-description: true
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Panoramica sulla distribuzione di Adobe Access Server for Protected Streaming {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Prima di distribuire Adobe Access Server for Protected Streaming, accertarsi di aver installato le versioni di Java e Tomcat elencate nella sezione Requisiti.

Il pacchetto Adobe Access Server for Protected Streaming include [!DNL flashaccesserver.war]. Per distribuire questo file WAR, copialo nel file Tomcat [!DNL webapps] directory. Se il file WAR è stato distribuito in precedenza, potrebbe essere necessario eliminare manualmente la directory WAR decompressa ( [!DNL flashaccessserver] in Tomcat [!DNL webapps] directory). Per evitare che Tomcat decomprima i file WAR, modificare la [!DNL server.xml] file in Tomcat [!DNL conf] e impostare `unpackWARs` attribuire a `false`.

>[!NOTE]
>
>Se hai configurato Tomcat per includere [!DNL commons-logging.jar] in System classpath (non richiesto per Adobe Access Server for Protected Streaming), commons-logging deve essere configurato per l&#39;utilizzo di Log4J.

Il server utilizza facoltativamente una libreria specifica della piattaforma ( [!DNL jsafe.dll] in Microsoft Windows o [!DNL libjsafe.so] su Linux) per prestazioni ottimali. Copia la libreria appropriata per la piattaforma da [!DNL thirdparty/cryptoj/]*piattaforma* in una posizione specificata da `PATH` variabile di ambiente (o `LD_LIBRARY_PATH` su Linux).

>[!NOTE]
>
>La versione a 64 bit deve essere utilizzata solo se sia il sistema operativo che JDK supportano la versione a 64 bit, altrimenti utilizzare la versione a 32 bit.
