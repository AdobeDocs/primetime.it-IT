---
title: Monitoraggio
description: Monitoraggio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Monitoraggio{#monitoring}

Il server Individualization e il server Key Generation dispongono ciascuno di una pagina di stato che puoi utilizzare per determinare lo stato dei server.

* **Pagina di stato dell’individualizzazione:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Segnala &quot;Alive&quot; se l&#39;app server è in esecuzione e l&#39;app può effettuare una richiesta di GET al server Key Generation
   * La pagina riporta &quot;Alive&quot; o nulla. Non viene visualizzata alcuna informazione sull&#39;applicazione, pertanto questa pagina può essere utilizzata per il monitoraggio dall&#39;esterno del firewall.

* **Pagina stato generazione chiave:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Segnala &quot;Alive&quot; se il server app è in esecuzione
   * Tutti gli URL di generazione delle chiavi devono essere accessibili solo internamente

* **Pagina Statistiche di individuazione:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Include statistiche sul server di Individualization, come il numero di richieste servite e il numero di chiavi disponibili nella cache
   * Questa pagina deve essere accessibile solo internamente

* **Pagina Statistiche di generazione chiave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Include statistiche sul server di generazione delle chiavi, come il numero di richieste servite e il numero di file chiave disponibili sul disco
   * Tutti gli URL di generazione delle chiavi devono essere accessibili solo internamente

