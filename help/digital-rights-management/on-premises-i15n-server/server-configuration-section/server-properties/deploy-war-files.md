---
seo-title: Distribuzione dei file WAR
title: Distribuzione dei file WAR
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Distribuzione dei file WAR{#deploy-the-war-files}

1. Copiare il file WAR nella [!DNL webapps] directory di Tomcat.

   * Server di individuazione: [!DNL flashaccess.war]
   * Server di generazione chiave: [!DNL flashaccess-kgs.war]

1. Copiate la [!DNL ROOT] cartella dal pacchetto fornito da Adobe alla [!DNL webapps] directory.

   Il server di individuazione deve inoltre ospitare il [!DNL crossdomain.xml] file. (La [!DNL ROOT] cartella contiene il [!DNL crossdomain.xml] file; deve [!DNL ROOT] essere in tutte le estremità.) Il server di generazione delle chiavi non richiede questo file.

