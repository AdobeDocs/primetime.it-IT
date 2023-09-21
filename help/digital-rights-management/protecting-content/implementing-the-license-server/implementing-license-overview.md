---
title: Panoramica del server licenze
description: Panoramica del server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Panoramica {#license-server-overview}

Prima di poter rilasciare licenze ai client, è necessario distribuire un server licenze Adobe Primetime DRM. Il server licenze utilizza l&#39;SDK DRM di Primetime per eseguire una serie di attività.

Per implementare un server licenze:

* Elabora richieste di autenticazione, se è supportata l’autenticazione nome utente/password.
* Elabora richieste di licenza
* Richieste Process Get Server Version: tutti i server devono implementare il supporto per questo tipo di richiesta.
* Elabora richieste di registrazione del dominio: necessario solo se si implementa un server di dominio.
* Elabora richieste di annullamento della registrazione dei domini: necessario solo se si implementa un server di dominio.
* Sincronizzazione dei processi: necessaria solo se le licenze specificano i requisiti di sincronizzazione.

Inoltre, il server deve fornire una regola di business per l’autenticazione degli utenti, per determinare se gli utenti sono autorizzati a visualizzare il contenuto e, facoltativamente, per tenere traccia dell’utilizzo delle licenze.

Consulta *Riferimento API di Adobe Primetime DRM* per informazioni dettagliate sull’API Java.
