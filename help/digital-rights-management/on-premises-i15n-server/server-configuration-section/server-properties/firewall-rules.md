---
seo-title: Regole firewall
title: Regole firewall
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Regole firewall{#firewall-rules}

Per proteggere l&#39;accesso al server di Individualizzazione, è necessario esporre solo alcuni percorsi dell&#39;applicazione. Il server di individuazione deve accettare le richieste dei client ai seguenti percorsi:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

I percorsi del servizio, come [!DNL /flashaccess/admin/*] (ovvero pagine di stato e di amministrazione) devono essere accessibili solo dall&#39;interno del firewall. Dall&#39;esterno del firewall non è possibile accedere ad alcuna parte del server di generazione delle chiavi.
