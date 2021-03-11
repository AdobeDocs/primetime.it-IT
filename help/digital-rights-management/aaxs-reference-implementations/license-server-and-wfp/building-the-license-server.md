---
title: Creazione del server licenze
description: Creazione del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Creazione del server licenze {#building-the-license-server}

Il server licenze di implementazione di riferimento include file WAR per la distribuzione del server licenze. Include anche tutto il codice sorgente del server di licenza e uno script Ant build (Riferimento Implementation\Server\refimpl\build-refimpl.xml) in modo da poter apportare facilmente modifiche al codice.

>[!NOTE]
>
>Questo passaggio è necessario solo se desideri modificare il codice sorgente. A scopo di valutazione, è possibile saltare questo passaggio e utilizzare i file WAR come spedito.

Prima di eseguire lo script Ant, modificare lo script per specificare le posizioni dell&#39;Adobe Access SDK, Tomcat, MySQL e Log4J. Apri build-refimpl.xml in un editor di testo e modifica i valori delle proprietà `sdkdir, tomcatdir, mysqldir, and log4jdir`. Per compilare il codice sorgente e creare i file WAR per l&#39;implementazione di riferimento, esegui lo script utilizzando `ant -f build-refimpl.xml all` nella directory contenente lo script Ant. Una volta completato lo script, verrà creata una directory [!DNL refimpl-build/wars] contenente i file WAR del server.
