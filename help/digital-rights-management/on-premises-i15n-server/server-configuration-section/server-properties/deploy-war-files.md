---
title: Distribuire i file WAR
description: Distribuire i file WAR
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Distribuire i file WAR{#deploy-the-war-files}

1. Copia il file WAR nella directory [!DNL webapps] di Tomcat.

   * Individualization Server: [!DNL flashaccess.war]
   * Server di generazione chiavi: [!DNL flashaccess-kgs.war]

1. Copia la cartella [!DNL ROOT] dal pacchetto fornito da Adobe nella directory [!DNL webapps] .

   Il server di Individualization deve inoltre ospitare il file [!DNL crossdomain.xml] . (La cartella [!DNL ROOT] contiene il file [!DNL crossdomain.xml]; [!DNL ROOT] deve essere in tutte le maiuscole.) Il file non è richiesto dal server di generazione della chiave.

