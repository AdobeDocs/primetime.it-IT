---
title: Opzioni di distribuzione del server licenze
description: Opzioni di distribuzione del server licenze
copied-description: true
exl-id: e06d59c0-517d-4483-9132-ceb37efada31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Opzioni di distribuzione del server licenze{#license-server-deployment-options}

È possibile distribuire il server licenze utilizzando una delle opzioni seguenti:

* Server Adobe Primetime DRM per lo streaming protetto: questo server licenze è ottimizzato per lo streaming. Ad Adobe, è possibile configurare il server HTTP Dynamic Streaming con Primetime DRM. Questo server può essere facilmente distribuito con una configurazione minima richiesta e supporta più tenant. Può raggiungere un elevato livello di scalabilità. Poiché questa implementazione è ottimizzata per lo streaming, non supporta tutte le funzioni DRM di Primetime. Ad esempio, l’autenticazione nome utente/password, i domini e il concatenamento delle licenze non sono supportati. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate tramite un file di configurazione del server, che sostituisce i criteri utilizzati al momento della creazione del pacchetto.

   Consulta la *Guida di Adobe Primetime DRM Server per lo streaming protetto* per ulteriori dettagli sulle regole di utilizzo supportate dal server licenze.
* Server licenze di implementazione di riferimento: è possibile utilizzare questa configurazione per personalizzare l&#39;implementazione del server. Questo è un esempio di implementazione del server licenze, con codice sorgente incluso, che illustra come utilizzare le API nell’SDK DRM di Primetime per gestire tutti i tipi di richieste e come implementare una logica di business personalizzata supportata da un database. Le regole di utilizzo nelle licenze rilasciate da questo server sono controllate dai criteri associati al contenuto al momento della creazione del pacchetto.
* Implementazione personalizzata del server: è inoltre possibile implementare il proprio server di licenze con l’SDK. Le informazioni descrivono come le API vengono utilizzate per implementare un server licenze.
