---
description: Un modo per coordinare la licenza e l'applicazione dei criteri consiste nel creare queste funzioni in un server di adesione.  Adobe fornisce il server di adesione di riferimento SEES con cui potete lavorare per creare il vostro server.
seo-description: Un modo per coordinare la licenza e l'applicazione dei criteri consiste nel creare queste funzioni in un server di adesione.  Adobe fornisce il server di adesione di riferimento SEES con cui potete lavorare per creare il vostro server.
seo-title: Server di riferimento ExpressPlay Entitlement Server (SEES) di esempio
title: Server di riferimento ExpressPlay Entitlement Server (SEES) di esempio
uuid: 99e42f76-7730-42fc-a9a9-f6396ac12c02
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Server di riferimento: Esempio di ExpressPlay Entitlement Server (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Un modo per coordinare la licenza e l&#39;applicazione dei criteri consiste nel creare queste funzioni in un server di adesione.  Adobe fornisce il server di adesione di riferimento SEES con cui potete lavorare per creare il vostro server.

Il server di riferimento SEES illustra il servizio di adesione ExpressPlay, con due servizi: adesione basata sull&#39;ora di base e adesione al binding del dispositivo.

Il SEES è basato su due servizi ExpressPlay Fairplay:

1. Servizio Richiesta token Expressplay
1. Expressplay Record Recupero Servizio

Il formato URL per la richiesta ExpressPlay Token ha due moduli, uno per la produzione e uno per l&#39;ambiente di prova:

**Produzione**: <span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Prova**: <span></span>https://fp-gen.test.expressplay.com/hms/fp/token

Il formato URL per il recupero di ExpressPlay Record richiede due moduli, uno per la produzione e uno per l&#39;ambiente di prova:

**Produzione**: <span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Prova**: <span></span>https://api.test.expressplay.com/cmiapi/getrecord/
