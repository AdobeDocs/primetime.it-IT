---
title: Distribuire i file WAR
description: Distribuire i file WAR
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# Distribuire i file WAR{#deploy-the-war-files}

1. Copiare il file WAR in Tomcat [!DNL webapps] directory.

   * Server di personalizzazione: [!DNL flashaccess.war]
   * Server di generazione chiavi: [!DNL flashaccess-kgs.war]

1. Copia il [!DNL ROOT] dal pacchetto fornito da Adobe alla cartella [!DNL webapps] directory.

   Il server di personalizzazione deve inoltre ospitare [!DNL crossdomain.xml] file. (Il [!DNL ROOT] la cartella contiene [!DNL crossdomain.xml] file; [!DNL ROOT] deve essere in maiuscolo.) Il server di generazione della chiave non richiede questo file.
