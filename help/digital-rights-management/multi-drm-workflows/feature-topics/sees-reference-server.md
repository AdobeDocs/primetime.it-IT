---
description: Un modo per coordinare la licenza e l'applicazione dei criteri consiste nel creare queste funzioni in un server di adesione. Adobe fornisce il server di adesione di riferimento SEES con cui puoi lavorare per creare il tuo server.
title: Server di riferimento di esempio ExpressPlay Entitlement Server (SEES)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Server di riferimento: Sample ExpressPlay Entitlement Server (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Un modo per coordinare la licenza e l&#39;applicazione dei criteri consiste nel creare queste funzioni in un server di adesione. Adobe fornisce il server di adesione di riferimento SEES con cui puoi lavorare per creare il tuo server.

Il server di riferimento SEES illustra il servizio di abilitazione ExpressPlay, con due servizi: adesione basata sull&#39;ora di base e adesione all&#39;associazione dispositivo.

Il SEES è basato su due servizi di riproduzione rapida ExpressPlay:

1. Servizio di richiesta del token Expressplay
1. Servizio di recupero record di Expressplay

Il formato URL per la richiesta di token ExpressPlay si compone di due moduli, uno per la produzione e uno per l’ambiente di test:

**Produzione**: <span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Test**: <span></span>https://fp-gen.test.expressplay.com/hms/fp/token

Il formato URL per il recupero dei record ExpressPlay richiede due moduli, uno per la produzione e uno per l&#39;ambiente di test:

**Produzione**: <span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Test**: <span></span>https://api.test.expressplay.com/cmiapi/getrecord/
