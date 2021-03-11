---
title: Panoramica sull'autenticazione/adesione personalizzata (facoltativo)
description: Panoramica sull'autenticazione/adesione personalizzata (facoltativo)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Panoramica sull&#39;autenticazione/adesione personalizzata (facoltativo){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM può essere configurato per contattare il tuo servizio di autenticazione/autorizzazione back-end per determinare:

* L’utente può acquistare una licenza?
* Quali diritti/restrizioni devono essere inseriti nella licenza?

Primetime Cloud DRM include un&#39;implementazione di riferimento di un servizio di autenticazione/adesione back-end. A scopo dimostrativo, questo server sta inviando risposte &quot;allow&quot; alle richieste BEES. Vedere [!DNL BEESServlet.java] per modificare il comportamento del server.

>[!NOTE]
>
>Precedentemente, si trattava di un prodotto separato denominato *Back End Entitlement Server* (BEES), quindi i riferimenti a BEES in tutto il documento e nei file di origine.

