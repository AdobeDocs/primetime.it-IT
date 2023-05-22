---
title: Creazione del server licenze
description: Creazione del server licenze
copied-description: true
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Creazione del server licenze {#building-the-license-server}

Il server licenze di implementazione di riferimento include file WAR per la distribuzione del server licenze. Include inoltre tutto il codice sorgente del server di licenze e uno script di generazione della formica (riferimento Implementation\Server\refimpl\build-refimpl.xml) che consente di apportare facilmente modifiche al codice.

>[!NOTE]
>
>Questo passaggio è necessario solo se desideri modificare il codice sorgente. A scopo di valutazione, puoi saltare questo passaggio e utilizzare i file WAR così come sono stati spediti.

Prima di eseguire lo script Ant, modificare lo script per specificare le posizioni dell&#39;SDK di accesso Adobe, Tomcat, MySQL e Log4J. Apri build-refimpl.xml in un editor di testo e modifica i valori delle proprietà `sdkdir, tomcatdir, mysqldir, and log4jdir`. Per compilare il codice sorgente e creare i file WAR per l’implementazione di riferimento, esegui lo script utilizzando `ant -f build-refimpl.xml all` nella directory contenente lo script Ant. Una volta completato lo script, [!DNL refimpl-build/wars] verrà creata una directory contenente i file WAR del server.
