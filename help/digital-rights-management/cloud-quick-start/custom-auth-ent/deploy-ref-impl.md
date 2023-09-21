---
title: Implementare l’implementazione di riferimento BEES
description: Implementare l’implementazione di riferimento BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# Implementare l’implementazione di riferimento BEES {#deploy-the-bees-reference-implementation}

1. Configurare il server applicazioni Tomcat. Consulta la documentazione di Tomcat.
1. Copia il `[!DNL bees.war]` archiviare in Tomcat [!DNL webapps/] cartella.
1. Inviare una richiesta a `https://localhost:8080/bees`.

   Se viene visualizzato il messaggio &quot;BEES is operating&quot; (BEES è operativo), la distribuzione viene completata correttamente.
1. Abilita SSL sul server.
