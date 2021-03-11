---
title: Regole firewall
description: Regole firewall
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Regole firewall{#firewall-rules}

Per proteggere l&#39;accesso al server Individualization, è necessario esporre solo alcuni percorsi applicativi. Il server di Individualization deve accettare le richieste dei client per i seguenti percorsi:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

I percorsi del servizio, ad esempio [!DNL /flashaccess/admin/*] (ovvero pagine di stato e di amministrazione) devono essere accessibili solo dall’interno del firewall. Non è possibile accedere a parti del server di generazione chiavi dall&#39;esterno del firewall.
