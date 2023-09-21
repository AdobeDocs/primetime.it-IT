---
title: Regole firewall
description: Regole firewall
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Regole firewall{#firewall-rules}

Per proteggere l&#39;accesso al server di personalizzazione, è necessario esporre solo alcuni percorsi dell&#39;applicazione. Il server di personalizzazione deve accettare le richieste dei client ai percorsi seguenti:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Percorsi di servizio, ad esempio [!DNL /flashaccess/admin/*] (ad esempio, le pagine di stato e di amministrazione) devono essere accessibili solo dall’interno del firewall. Nessuna parte del server di generazione delle chiavi deve essere accessibile dall&#39;esterno del firewall.
