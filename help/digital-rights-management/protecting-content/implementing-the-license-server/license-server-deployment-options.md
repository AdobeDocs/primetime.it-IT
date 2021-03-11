---
title: Opzioni di distribuzione del server licenze
description: Opzioni di distribuzione del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Opzioni di distribuzione del server licenze{#license-server-deployment-options}

È possibile distribuire il server licenze utilizzando una delle seguenti opzioni:

* Server DRM Adobe Primetime per streaming protetto - Questo server licenze è ottimizzato per lo streaming. Ad Adobe, è possibile configurare il server con Primetime DRM per HTTP Dynamic Streaming. Questo server può essere facilmente implementato con una configurazione molto ridotta richiesta e supporta più tenant. Può raggiungere un alto livello di scalabilità. Poiché questa implementazione è ottimizzata per lo streaming, non supporta le funzioni DRM di Primetime complete. Ad esempio, l’autenticazione nome utente/password, i domini e il concatenamento delle licenze non sono supportati. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite un file di configurazione del server, che sostituisce il criterio utilizzato al momento della creazione del pacchetto.

   Per ulteriori informazioni sulle regole di utilizzo supportate dal server delle licenze, vedere la *Guida al server DRM di Adobe Primetime per lo streaming protetto* .
* Riferimento al server licenze di implementazione: puoi utilizzare questa configurazione per personalizzare l&#39;implementazione del server. Questo è un esempio di implementazione del server di licenze, incluso il codice sorgente, che dimostra come utilizzare le API nell’SDK DRM di Primetime per gestire tutti i tipi di richieste e come implementare la logica di business personalizzata supportata da un database. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite i criteri associati al contenuto al momento dell&#39;imballaggio.
* Implementazione del server personalizzato - Puoi anche implementare il server licenze personalizzato con l&#39;SDK. Le informazioni descrivono come le API vengono utilizzate per implementare un server di licenze.

