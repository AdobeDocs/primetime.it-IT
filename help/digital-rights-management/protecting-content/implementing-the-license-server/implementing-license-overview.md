---
seo-title: Panoramica del server licenze
title: Panoramica del server licenze
uuid: 8c62376b-b159-4297-9322-75d62947e84e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Panoramica {#license-server-overview}

Prima di rilasciare licenze ai client, è necessario distribuire un server licenze Adobe Primetime DRM. Il server licenze utilizza l&#39;SDK DRM di Primetime per eseguire una serie di attività.

Per implementare un server licenze:

* Elabora le richieste di autenticazione, se è supportata l&#39;autenticazione tramite nome utente e password.
* Elabora richieste di licenza
* Elabora richieste Get Server Version: tutti i server devono implementare il supporto per questo tipo di richiesta.
* Elabora richieste di registrazione del dominio - Necessario solo se si implementa un server di dominio.
* Elabora richieste di cancellazione del dominio - Necessario solo se si implementa un server di dominio.
* Sincronizzazione dei processi: necessaria solo se le licenze specificano i requisiti di sincronizzazione.

Inoltre, il server deve fornire una logica aziendale per l&#39;autenticazione degli utenti, determinare se gli utenti sono autorizzati a visualizzare il contenuto e, facoltativamente, monitorare l&#39;utilizzo delle licenze.

Consultate *Adobe Primetime DRM API Reference* (Riferimento API DRM di Adobe Primetime) per informazioni dettagliate sull&#39;API Java.
