---
title: Panoramica sulla distribuzione del server licenze e del packager delle cartelle controllate
description: Panoramica sulla distribuzione del server licenze e del packager delle cartelle controllate
copied-description: true
exl-id: b44aec8b-f1d7-4dce-bc51-0ce2b74ae0c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Panoramica sulla distribuzione del server licenze e del packager delle cartelle controllate {#deploying-the-license-server-and-watched-folder-packager-overview}

Copiare i file WAR del server licenze in Tomcat [!DNL webapps] directory. Se il file WAR è stato distribuito in precedenza, potrebbe essere necessario eliminare manualmente le directory WAR decompresse ( [!DNL flashaccess], [!DNL edcws], e [!DNL flashaccess-packager] in Tomcat [!DNL webapps] directory). Per evitare che Tomcat decomprima i file WAR, modificare la [!DNL server.xml] nella directory conf di Tomcat e impostare `unpackWARs` attribuire a `false`.

Il file delle proprietà ( [!DNL flashaccess-refimpl.properties]) deve trovarsi nel classpath affinché il server possa caricare le proprietà. Copiare il file in una directory e aggiornarlo con i valori appropriati. Modifica il [!DNL catalina.properties] file in Tomcat [!DNL conf] e aggiungere la directory contenente [!DNL flashaccess-refimpl.properties] al `shared.loader` proprietà. Il [!DNL log4j.xml] il file per la configurazione della registrazione deve trovarsi anche sul classpath (vedere [!DNL resources\log4j.xml] ad esempio).

Il server di implementazione di riferimento utilizza diversi file di certificato, file di criteri e altre risorse. Tali file si trovano tutti in una cartella di risorse. Per impostazione predefinita, la cartella delle risorse è [!DNL C:\flashaccess-server-resources], ma questa posizione può essere modificata in [!DNL flashaccess-refimpl.properties]. Accertarsi di copiare tutte le risorse richieste in questa posizione prima di avviare il server.

Per avviare Tomcat e il server licenze, eseguire `catalina.bat start` da Tomcat [!DNL bin] directory.
