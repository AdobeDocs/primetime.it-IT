---
title: Opzioni di distribuzione del server licenze
description: Opzioni di distribuzione del server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Opzioni di distribuzione del server licenze{#license-server-deployment-options}

Il server licenze può essere distribuito utilizzando una delle opzioni seguenti:

* **Adobe Access Server per Streaming protetto** — Questo server licenze è ottimizzato per lo streaming. È ad esempio possibile configurare il server, ad Adobe HTTP Dynamic Streaming, con Adobe Access. Questo server può essere facilmente implementato con una configurazione molto ridotta, supporta più tenant e può raggiungere un elevato livello di scalabilità. Tuttavia, poiché questa implementazione è ottimizzata per lo streaming, non supporta le funzioni complete di accesso agli Adobi. Ad esempio, l’autenticazione nome utente/password, i domini e il concatenamento delle licenze non sono supportati. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite un file di configurazione del server, che sostituisce i criteri utilizzati al momento della creazione del pacchetto. Consulta la *Guida di Adobe Access Server per Streaming protetto* per ulteriori dettagli sulle regole di utilizzo supportate da questo server.
* **Server licenze di implementazione di riferimento** — Utilizzare questa configurazione come punto di partenza per un&#39;implementazione server personalizzata. Si tratta di un esempio di implementazione del server licenze, incluso il codice sorgente, che illustra come utilizzare le API nell’SDK di Access di Adobe per gestire tutti i tipi di richieste e come implementare una logica di business personalizzata supportata da un database. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate dai criteri associati al contenuto al momento della creazione del pacchetto.
* **Implementazione server personalizzata** — È inoltre possibile implementare il proprio server di licenze utilizzando l&#39;SDK. Le informazioni contenute in questo capitolo descrivono le API utilizzate per implementare un server licenze.
