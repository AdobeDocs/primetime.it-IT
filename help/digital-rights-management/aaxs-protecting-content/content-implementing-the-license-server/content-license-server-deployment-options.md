---
title: Opzioni di distribuzione del server licenze
description: Opzioni di distribuzione del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Opzioni di distribuzione del server licenze{#license-server-deployment-options}

Il server licenze può essere distribuito utilizzando una delle seguenti opzioni:

* **Adobe Access Server per streaming**  protetto: questo server licenze è ottimizzato per lo streaming. Ad esempio, è possibile configurare il server per Adobe HTTP Dynamic Streaming con accesso Adobe. Questo server può essere implementato facilmente con una configurazione molto limitata e supporterà più tenant e può raggiungere un alto livello di scalabilità. Tuttavia, poiché questa implementazione è ottimizzata per lo streaming, non supporta tutte le funzioni di accesso agli Adobi. Ad esempio, l’autenticazione nome utente/password, i domini e il concatenamento delle licenze non sono supportati. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite un file di configurazione del server, che sostituisce il criterio utilizzato al momento della creazione del pacchetto. Per ulteriori informazioni sulle regole di utilizzo supportate da questo server, consulta la *Adobe Access Server for Protected Streaming Guide* .
* **Server licenze di implementazione di riferimento** : utilizza questa configurazione come punto di partenza per un&#39;implementazione server personalizzata. Questo è un esempio di implementazione del server di licenze, incluso il codice sorgente, che illustra come utilizzare le API nell’SDK di Adobe Access per gestire tutti i tipi di richieste e come implementare la logica di business personalizzata supportata da un database. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite i criteri associati al contenuto al momento dell&#39;imballaggio.
* **Implementazione del server personalizzato** : puoi anche implementare un server licenze personalizzato utilizzando l&#39;SDK. Le informazioni contenute in questo capitolo descrivono le API utilizzate per implementare un server licenze.

