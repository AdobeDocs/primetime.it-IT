---
seo-title: Panoramica sulla distribuzione di Adobe Access Server per lo streaming protetto
title: Panoramica sulla distribuzione di Adobe Access Server per lo streaming protetto
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Panoramica sulla distribuzione di Adobe Access Server per lo streaming protetto {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Prima di distribuire Adobe Access Server per lo streaming protetto, accertatevi di aver installato le versioni di Java e Tomcat elencate nella sezione Requisiti.

Il pacchetto Adobe Access Server per lo streaming protetto include [!DNL flashaccesserver.war]. Per distribuire questo file WAR, copiatelo nella [!DNL webapps] directory di Tomcat. Se avete già distribuito il file WAR in precedenza, potrebbe essere necessario eliminare manualmente la directory WAR non imballata ( [!DNL flashaccessserver] nella directory di Tomcat [!DNL webapps] ). Per impedire a Tomcat di disfare i file WAR, modificare il [!DNL server.xml] file nella [!DNL conf] directory di Tomcat e impostare l&#39; `unpackWARs` attributo su `false`.

>[!NOTE]
>
>Se avete configurato Tomcat per l&#39;inclusione [!DNL commons-logging.jar] nel percorso di classe di sistema (non richiesto per Adobe Access Server per lo streaming protetto), la registrazione commons deve essere configurata per l&#39;utilizzo di Log4J.

Il server utilizza facoltativamente una libreria specifica per la piattaforma ( [!DNL jsafe.dll] in Microsoft Windows o [!DNL libjsafe.so] in Linux) per ottenere prestazioni ottimali. Copiate la libreria appropriata per la piattaforma dalla [!DNL thirdparty/cryptoj/]*piattaforma *alla posizione specificata dalla variabile di`PATH`ambiente (o`LD_LIBRARY_PATH`su Linux).

>[!NOTE]
>
>La versione a 64 bit deve essere utilizzata solo se il sistema operativo e il JDK supportano la versione a 64 bit, altrimenti utilizza la versione a 32 bit.

