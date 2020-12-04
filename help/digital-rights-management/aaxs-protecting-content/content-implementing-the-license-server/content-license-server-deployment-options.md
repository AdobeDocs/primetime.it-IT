---
seo-title: Opzioni di distribuzione del server licenze
title: Opzioni di distribuzione del server licenze
uuid: 297c587f-23e2-4bb5-911b-72d7b82370f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Opzioni di distribuzione del server licenze{#license-server-deployment-options}

Il server licenze può essere distribuito utilizzando una delle seguenti opzioni:

* **Adobe Access Server per lo streaming**  protetto: questo server di licenze è ottimizzato per lo streaming. Ad esempio, potete configurare il server per  HTTP Dynamic Streaming Adobe con  accesso Adobe. Questo server può essere facilmente implementato con una configurazione molto limitata e sarà in grado di supportare più tenant, e può raggiungere un alto livello di scalabilità. Tuttavia, poiché questa implementazione è ottimizzata per lo streaming, non supporta le funzioni di accesso  Adobe complete. Ad esempio, autenticazione tramite nome utente/password, domini e concatenamento di licenze non sono supportati. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite un file di configurazione del server, che sostituisce il criterio utilizzato al momento della creazione del pacchetto. Per ulteriori informazioni sulle regole di utilizzo supportate da questo server, vedere la *Guida allo streaming protetto di Adobe Access Server*.
* **Server**  licenze di implementazione di riferimento: utilizzate questa configurazione come punto di partenza per un&#39;implementazione server personalizzata. Si tratta di un esempio di implementazione del server delle licenze, incluso il codice sorgente, che illustra come utilizzare le API nell&#39;SDK di accesso al Adobe  per gestire tutti i tipi di richieste e come implementare la logica aziendale personalizzata supportata da un database. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite il criterio associato al contenuto al momento della creazione del pacchetto.
* **Implementazione**  server personalizzata: puoi anche implementare un server licenze personalizzato tramite l’SDK. Le informazioni riportate in questo capitolo descrivono le API utilizzate per implementare un server licenze.

