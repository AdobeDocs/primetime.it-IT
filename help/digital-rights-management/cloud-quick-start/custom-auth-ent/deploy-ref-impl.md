---
title: Implementazione del riferimento API
description: Implementazione del riferimento API
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# Implementazione del riferimento API {#deploy-the-bees-reference-implementation}

1. Imposta il server dell&#39;applicazione Tomcat. (Vedi la tua documentazione Tomcat.)
1. Copia il file `[!DNL bees.war]` nella cartella [!DNL webapps/] di Tomcat.
1. Invia una richiesta a `https://localhost:8080/bees`.

   Se viene visualizzato il messaggio &quot;BEES is operative&quot; (L’API è operativa), la distribuzione viene completata correttamente.
1. Abilita SSL sul server.
