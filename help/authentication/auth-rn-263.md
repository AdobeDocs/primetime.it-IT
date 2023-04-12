---
title: Note sulla versione di Adobe Primetime authentication 2.63
description: Note sulla versione di Adobe Primetime authentication 2.63
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Note sulla versione di Adobe Primetime Authentication 2.63 {#pt-authn-263-rn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione:

## Client lato server e Web {#server-side-web-clients-263}

* [Numero build](#build-number)
* [Nuove funzioni](#new-features)

### Numero build {#build-number-263}

Autenticazione Adobe Primetime: adobe-pass-**2,63**
Data di rilascio: **20/09/2022 - 22/09/2022**

### Nuove funzioni {#new-features-263}

#### Miglioramento del meccanismo di identificazione della piattaforma {#pf-identification-mech}

* A partire da questa versione, è stato migliorato il meccanismo utilizzato per identificare un dispositivo e non dipenderà più dall’implementazione lato client. Questo fornirà una granularità più precisa quando si applicano le regole di business a livello di piattaforma e una migliore comprensione dei valori di traffico nei report ESM.

* Presto verrà rilasciata una nuova versione di ESM con rapporti nuovi e migliorati che espongono i campi relativi alla piattaforma.

* Per maggiori dettagli sulle modifiche pianificate, contatta il tuo TAM.

#### Auto-degradazione MVPD {#mvpd-self-degradation}

Questa funzione fornisce agli MVPD la possibilità di bypassare temporaneamente gli endpoint di autenticazione e autorizzazione per gli scenari di traffico elevato quando il carico su questi rispettivi punti finali diventa troppo alto.


#### Aggiungi un ID proxy nell&#39;intestazione delle chiamate di autorizzazione {#add-proxied-id}

Questa funzione aggiunge l&#39;id di un MVPD proxy di Synacor nell&#39;intestazione della chiamata di autorizzazione. Questo consente a Synacor di impostare regole aziendali per ogni singolo proxy (ad esempio. indirizzamento a diversi domini per MVPD (proxy MVPD).


#### Dashboard TVE {#tve-dashboard}

In questa versione è stato risolto un problema a causa del quale authN o authZ TTL impostato a livello di MVPD non venivano calcolate correttamente nei rapporti di configurazione.


#### SDK JavaScript 4.6.0 {#js-sdk}

* È stato rimosso l’utilizzo di `eval` , rendendo l’SDK conforme ai criteri sulla sicurezza dei contenuti.
* È stato risolto un problema che impediva il completamento del flusso di autenticazione con esito positivo quando lo spazio di archiviazione locale del browser veniva esplicitamente cancellato da un&#39;applicazione partner.



