---
title: Regole firewall
description: Regole firewall
copied-description: true
exl-id: 1a40822a-893d-43ec-9c3e-8e0b4ebe6d01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
