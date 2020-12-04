---
seo-title: Opzioni di distribuzione del server licenze
title: Opzioni di distribuzione del server licenze
uuid: 732b948f-8037-423e-9f85-770d6316cbae
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Opzioni di distribuzione del server licenze{#license-server-deployment-options}

È possibile distribuire il server licenze utilizzando una delle seguenti opzioni:

*  Adobe Primetime DRM Server for Protected Streaming: questo server licenze è ottimizzato per lo streaming. Ad esempio, potete configurare il server per  HTTP Dynamic Streaming Adobe con Primetime DRM. Questo server può essere facilmente implementato con una configurazione molto limitata e supporta più tenant. Può raggiungere un elevato livello di scalabilità. Poiché questa implementazione è ottimizzata per lo streaming, non supporta tutte le funzioni DRM di Primetime. Ad esempio, autenticazione tramite nome utente/password, domini e concatenamento di licenze non sono supportati. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite un file di configurazione del server, che sostituisce il criterio utilizzato al momento della creazione del pacchetto.

   Per ulteriori informazioni sulle regole di utilizzo supportate dal server licenze, vedere la *Adobe Primetime DRM Server for Protected Streaming Guide*.
* Server licenze di implementazione di riferimento: puoi utilizzare questa configurazione per personalizzare l&#39;implementazione del server. Si tratta di un esempio di implementazione del server delle licenze, incluso il codice sorgente, che illustra come utilizzare le API nell&#39;SDK DRM di Primetime per gestire tutti i tipi di richieste e come implementare la logica aziendale personalizzata supportata da un database. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite il criterio associato al contenuto al momento della creazione del pacchetto.
* Implementazione server personalizzata (Custom Server Implementation) - Potete anche implementare un vostro server licenze con l&#39;SDK. Le informazioni descrivono in che modo le API vengono utilizzate per implementare un server licenze.

