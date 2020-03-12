---
seo-title: Panoramica
title: Panoramica
uuid: f4ae10ca-6e2a-4313-80a0-4c7377dba000
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Panoramica{#overview}

Per rilasciare licenze ai client, è necessario distribuire un server licenze Adobe Access. Il server licenze utilizza l&#39;SDK Adobe® Access™ per eseguire le seguenti attività:

* Elabora le richieste di autenticazione, se è supportata l&#39;autenticazione tramite nome utente e password.
* Elabora richieste di licenza
* Elabora richieste Get Server Version: tutti i server devono implementare il supporto per questo tipo di richiesta.
* Elabora richieste di registrazione del dominio: necessarie solo se si implementa un server di dominio.
* Elabora richieste di cancellazione del dominio: necessarie solo se si implementa un server di dominio.
* Sincronizzazione processo: necessaria solo se le licenze specificano i requisiti di sincronizzazione.

Inoltre, il server deve fornire una logica aziendale per l&#39;autenticazione degli utenti, determinare se gli utenti sono autorizzati a visualizzare il contenuto e, facoltativamente, monitorare l&#39;utilizzo delle licenze.

Per informazioni dettagliate sulle API Java discusse in questo capitolo, consultate Guida di riferimento *alle API di* Adobe Access.
