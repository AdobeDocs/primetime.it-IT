---
seo-title: Monitoraggio
title: Monitoraggio
uuid: ee62c55f-0d44-40f4-a2c7-39456f4d3d99
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Monitoring{#monitoring}

Il server di individuazione e il server di generazione delle chiavi dispongono ciascuna di una pagina di stato, che potete utilizzare per determinare lo stato dei server.

* **Pagina di stato dell&#39;individuazione:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Segnala &quot;Vivo&quot; se il server app è in esecuzione e l’app può effettuare una richiesta di GET al server di generazione chiave
   * La pagina riporta &quot;Vivo&quot; o &quot;Nulla&quot;. Non vengono visualizzate informazioni sull&#39;applicazione, pertanto questa pagina potrebbe essere utilizzata per il monitoraggio dall&#39;esterno del firewall.

* **Pagina Stato generazione chiave:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Segnala &quot;Vivo&quot; se il server app è in esecuzione
   * Tutti gli URL di generazione delle chiavi devono essere accessibili solo internamente

* **Pagina Statistiche di individuazione:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Include statistiche sul server di individuazione, come il numero di richieste servite e il numero di chiavi disponibili nella cache
   * Questa pagina deve essere accessibile solo internamente

* **Pagina Statistiche generazione chiave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Include statistiche sul server di generazione delle chiavi, come il numero di richieste servite e il numero di file chiave disponibili sul disco
   * Tutti gli URL di generazione delle chiavi devono essere accessibili solo internamente

