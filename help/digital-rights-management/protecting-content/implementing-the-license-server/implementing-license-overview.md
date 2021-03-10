---
title: Panoramica del server licenze
description: Panoramica del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Panoramica {#license-server-overview}

Prima di poter rilasciare licenze ai clienti, devi distribuire un server di licenze Adobe Primetime DRM. Il server di licenze utilizza l&#39;SDK DRM di Primetime per eseguire diverse attività.

Per implementare un server licenze:

* Elabora le richieste di autenticazione, se è supportata l’autenticazione con nome utente e password.
* Richieste di licenza del processo
* Elabora richieste Get Server Version: tutti i server devono implementare il supporto per questo tipo di richiesta.
* Elabora richieste di registrazione del dominio - Necessario solo se si implementa un server di dominio.
* Elabora richieste di cancellazione del dominio - Necessario solo se si implementa un server di dominio.
* Sincronizzazione del processo: necessaria solo se le licenze specificano i requisiti di sincronizzazione.

Inoltre, il server deve fornire una logica di business per l’autenticazione degli utenti, determinare se gli utenti sono autorizzati a visualizzare il contenuto e, facoltativamente, tenere traccia dell’utilizzo della licenza.

Per informazioni dettagliate sull&#39;API Java, consulta *Riferimento API DRM di Adobe Primetime* .
