---
title: Panoramica su autenticazione/adesione personalizzata (facoltativo)
description: Panoramica su autenticazione/adesione personalizzata (facoltativo)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
