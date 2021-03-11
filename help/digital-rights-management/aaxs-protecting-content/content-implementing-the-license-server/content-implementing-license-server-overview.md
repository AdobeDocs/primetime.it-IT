---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Panoramica{#overview}

Per rilasciare licenze ai client, è necessario distribuire un server licenze di Adobe Access. Il server licenze utilizza l&#39;SDK Adobe® Access™ per eseguire queste attività:

* Elabora le richieste di autenticazione, se è supportata l’autenticazione con nome utente e password.
* Richieste di licenza del processo
* Elabora richieste Get Server Version: tutti i server devono implementare il supporto per questo tipo di richiesta.
* Elabora richieste di registrazione del dominio - Necessario solo se si implementa un server di dominio.
* Elabora richieste di cancellazione del dominio - Necessario solo se si implementa un server di dominio.
* Sincronizzazione del processo: necessaria solo se le licenze specificano i requisiti di sincronizzazione.

Inoltre, il server deve fornire una logica di business per l’autenticazione degli utenti, determinare se gli utenti sono autorizzati a visualizzare il contenuto e, facoltativamente, tenere traccia dell’utilizzo della licenza.

Per informazioni dettagliate sull&#39;API Java discussa in questo capitolo, consulta *Riferimento API di accesso agli Adobi*.
