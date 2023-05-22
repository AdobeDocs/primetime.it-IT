---
title: Panoramica su autenticazione/adesione personalizzata (facoltativo)
description: Panoramica su autenticazione/adesione personalizzata (facoltativo)
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Panoramica su autenticazione/adesione personalizzata (facoltativo){#custom-authentication-entitlement-overview-optional}

È possibile configurare Primetime Cloud DRM per raggiungere il servizio di autenticazione/adesione back-end per determinare:

* Questo utente può acquistare una licenza?
* Quali diritti/restrizioni devono essere inclusi nella licenza?

Primetime Cloud DRM include un’implementazione di riferimento di un servizio di autenticazione/adesione back-end. A scopo dimostrativo, questo server sta fornendo risposte &quot;consentite&quot; alle richieste di BEES. Consulta [!DNL BEESServlet.java] per modificare il comportamento del server.

>[!NOTE]
>
>In precedenza, questo era un prodotto separato denominato *Server di adesione back-end* (API), quindi i riferimenti alle API in tutto il presente documento e nei file di origine.
