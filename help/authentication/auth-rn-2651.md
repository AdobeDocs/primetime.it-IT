---
title: Note sulla versione di Adobe Pass Authentication 2.65.1
description: Note sulla versione di Adobe Pass Authentication 2.65.1
source-git-commit: c8259e3268556c20630fff92aa90b0f7f9c12617
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Note sulla versione di Adobe Pass Authentication 2.65.1 {#authn-2651-rn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione:

## Client Web e lato server {#server-side-web-clients-2651}

* [Numero build](#build-number-2651)
* [Panoramica sulla versione](#release-overview-2651)

### Numero build {#build-number-2651}

Autenticazione Adobe Pass: adobe-pass-**2.65.1**
Data di rilascio: **06/20/2023 - 06/22/2023**

### Panoramica sulla versione {#release-overview-2651}

Questa versione aggiunge quanto segue:

A partire da questa versione verrà introdotto il supporto tecnico per aggiungere regole di limitazione della velocità in tutte le API, al fine di proteggere l’ecosistema complessivo da un utilizzo errato.

L’obiettivo iniziale è monitorare il comportamento delle applicazioni per stabilire i valori limite appropriati e non verranno applicati limiti nell’ambito di questa versione. Nei casi in cui il traffico generato da una specifica applicazione superi determinati limiti, collaboreremo con ciascun cliente per convalidare l’implementazione.

Le regole di limitazione della tariffa verranno applicate più avanti nel corso dell’anno, dopo la convalida del traffico generato da tutte le applicazioni del cliente.
