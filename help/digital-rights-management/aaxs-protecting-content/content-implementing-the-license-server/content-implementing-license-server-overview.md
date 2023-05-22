---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Panoramica{#overview}

Per rilasciare licenze ai client, è necessario distribuire un server licenze Adobe Access. Il server licenze utilizza l&#39;SDK Adobe® Access™ per eseguire le seguenti attività:

* Elabora richieste di autenticazione, se è supportata l’autenticazione nome utente/password.
* Elabora richieste di licenza
* Richieste Process Get Server Version: tutti i server devono implementare il supporto per questo tipo di richiesta.
* Elabora richieste di registrazione del dominio: necessario solo se si implementa un server di dominio.
* Elabora richieste di annullamento della registrazione dei domini: necessario solo se si implementa un server di dominio.
* Sincronizzazione dei processi - Necessario solo se le licenze specificano i requisiti di sincronizzazione.

Inoltre, il server deve fornire una regola di business per l’autenticazione degli utenti, per determinare se gli utenti sono autorizzati a visualizzare il contenuto e, facoltativamente, per tenere traccia dell’utilizzo delle licenze.

Per informazioni dettagliate sull’API Java descritta in questo capitolo, consulta *Riferimento API per l’accesso agli Adobi*.
