---
title: Panoramica sulla distribuzione di Adobe Access Server per lo streaming protetto
description: Panoramica sulla distribuzione di Adobe Access Server per lo streaming protetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Panoramica sulla distribuzione di Adobe Access Server per lo streaming protetto {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Prima di distribuire Adobe Access Server per lo streaming protetto, assicurati di aver installato le versioni di Java e Tomcat elencate nella sezione Requisiti.

Il pacchetto Adobe Access Server per lo streaming protetto include [!DNL flashaccesserver.war]. Per distribuire questo file WAR, copialo nella directory [!DNL webapps] di Tomcat. Se in precedenza hai implementato il file WAR, potrebbe essere necessario eliminare manualmente la directory WAR decompressa ( [!DNL flashaccessserver] nella directory [!DNL webapps] di Tomcat). Per evitare che Tomcat scompili i file WAR, modifica il file [!DNL server.xml] nella directory [!DNL conf] di Tomcat e imposta l&#39;attributo `unpackWARs` su `false`.

>[!NOTE]
>
>Se hai configurato Tomcat in modo da includere [!DNL commons-logging.jar] nel percorso di classe del sistema (non necessario per Adobe Access Server per lo streaming protetto), la registrazione di contenuti condivisi deve essere configurata per utilizzare Log4J.

Il server utilizza facoltativamente una libreria specifica per la piattaforma ( [!DNL jsafe.dll] in Microsoft Windows o [!DNL libjsafe.so] su Linux) per ottenere prestazioni ottimali. Copia la libreria appropriata per la piattaforma da [!DNL thirdparty/cryptoj/]*platform* in una posizione specificata dalla variabile di ambiente `PATH` (o `LD_LIBRARY_PATH` su Linux).

>[!NOTE]
>
>La versione a 64 bit deve essere utilizzata solo se sia il sistema operativo che JDK supportano 64-bit, altrimenti utilizza la versione a 32 bit.

