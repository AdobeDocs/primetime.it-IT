---
seo-title: Distribuzione dei file WAR
title: Distribuzione dei file WAR
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Distribuzione di file WAR{#deploy-the-war-files}

1. Copiare il file WAR nella directory [!DNL webapps] di Tomcat.

   * Server di individuazione: [!DNL flashaccess.war]
   * Server di generazione chiave: [!DNL flashaccess-kgs.war]

1. Copiate la cartella [!DNL ROOT] dal pacchetto fornito da  Adobe alla directory [!DNL webapps].

   Il server di individuazione deve inoltre ospitare il file [!DNL crossdomain.xml]. (La cartella [!DNL ROOT] contiene il file [!DNL crossdomain.xml]; [!DNL ROOT] deve trovarsi in tutte le estremità. Il server di generazione delle chiavi non richiede questo file.

