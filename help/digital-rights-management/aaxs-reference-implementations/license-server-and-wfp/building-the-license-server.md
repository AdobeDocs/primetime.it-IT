---
seo-title: Creazione del server licenze
title: Creazione del server licenze
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Creazione del server licenze {#building-the-license-server}

Il server licenze di implementazione di riferimento include i file WAR per la distribuzione del server licenze. Include inoltre tutto il codice sorgente del server delle licenze e uno script di build Ant (Riferimento Implementation\Server\refimpl\build-refimpl.xml) per apportare facilmente modifiche al codice.

>[!NOTE]
>
>Questo passaggio è necessario solo se si desidera modificare il codice sorgente. A fini di valutazione, potete saltare questo passaggio e utilizzare i file WAR come spediti.

Prima di eseguire lo script Ant, modificare lo script per specificare le posizioni dell&#39;SDK di accesso al Adobe , Tomcat, MySQL e Log4J. Aprite build-refimpl.xml in un editor di testo e modificate i valori delle proprietà `sdkdir, tomcatdir, mysqldir, and log4jdir`. Per compilare il codice sorgente e creare i file WAR per l&#39;implementazione del riferimento, eseguire lo script utilizzando `ant -f build-refimpl.xml all` nella directory contenente lo script Ant. Al termine dello script, verrà creata una [!DNL refimpl-build/wars] directory contenente i file WAR del server.
