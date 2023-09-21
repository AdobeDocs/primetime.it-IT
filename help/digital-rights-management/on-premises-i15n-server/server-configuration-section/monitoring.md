---
title: Monitorare
description: Monitorare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Monitorare{#monitoring}

Sia il server di personalizzazione che il server di generazione della chiave dispongono di una pagina di stato che è possibile utilizzare per determinare l&#39;integrità dei server.

* **Pagina Stato di personalizzazione:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Segnala &quot;Vivo&quot; se il server dell’app è in esecuzione e l’app può effettuare una richiesta di GET al server di generazione della chiave
   * La pagina riporta &quot;Vivo&quot; o niente. Non viene rivelata alcuna informazione sull’applicazione, pertanto questa pagina potrebbe essere utilizzata per il monitoraggio dall’esterno del firewall.

* **Pagina stato generazione chiave:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Segnala &quot;Vivo&quot; se il server dell’app è in esecuzione
   * Tutti gli URL di generazione della chiave devono essere accessibili solo internamente

* **Pagina Statistiche di personalizzazione:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Include statistiche sul server di personalizzazione, ad esempio il numero di richieste inviate e il numero di chiavi disponibili nella cache
   * Questa pagina deve essere accessibile solo internamente

* **Pagina Statistiche di generazione chiave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Include statistiche sul server di generazione delle chiavi, ad esempio il numero di richieste inviate e il numero di file chiave disponibili su disco
   * Tutti gli URL di generazione della chiave devono essere accessibili solo internamente
