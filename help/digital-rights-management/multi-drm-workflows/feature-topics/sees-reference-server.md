---
description: Un modo per coordinare l’applicazione delle licenze e delle policy consiste nell’integrare queste funzioni in un server di adesione. L'Adobe fornisce il server di adesione di riferimento SEES con cui è possibile lavorare per creare il proprio server.
title: Esempio di server di riferimento per il server dei diritti ExpressPlay (SEES)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Server di riferimento: Sample ExpressPlay Entitlement Server (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Un modo per coordinare l’applicazione delle licenze e delle policy consiste nell’integrare queste funzioni in un server di adesione. L&#39;Adobe fornisce il server di adesione di riferimento SEES con cui è possibile lavorare per creare il proprio server.

Il server di riferimento SEES illustra il servizio di adesione ExpressPlay, che offre due servizi: adesione basata sul tempo di base e adesione al binding dei dispositivi.

Il SEES si basa su due servizi ExpressPlay Fairplay:

1. Servizio di richiesta token di espressione
1. Servizio di recupero record espressione

Il formato URL per la richiesta del token ExpressPlay assume due forme, una per la produzione e l’altra per l’ambiente di test:

**Produzione**: ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**Test**: ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

Il formato URL per il recupero dei record ExpressPlay assume due forme, una per la produzione e una per l’ambiente di test:

**Produzione**: ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**Test**: ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
