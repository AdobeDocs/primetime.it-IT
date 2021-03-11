---
title: Panoramica sulle api
description: Panoramica sulle api
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Panoramica API{#bees-overview}

È possibile implementare un servizio di adesione back-end (BEES) per fornire l&#39;adesione personalizzata per il funzionamento DRM di Primetime Cloud.

Primetime Cloud DRM utilizza la consegna anonima della licenza per impostazione predefinita. Ciò significa che tutte le richieste di licenza inviate a Primetime Cloud DRM restituiranno una licenza valida senza eseguire ulteriori controlli di autenticazione/autorizzazione (a meno che non sia stato applicato un vincolo di policy che richiede l’utilizzo dell’autenticazione Adobe Primetime).

La richiesta di licenza contiene la politica DRM utilizzata durante il packaging / crittografia del contenuto. Il criterio DRM viene utilizzato per generare la licenza DRM restituita al client. Nello scenario predefinito, è necessario prendere tutte le decisioni di policy DRM in fase di creazione del contenuto. I clienti che desiderano un controllo più preciso su questi flussi di lavoro possono scegliere tra le seguenti opzioni:

1. È possibile integrare l’autenticazione Primetime per aggiungere ulteriori controlli di adesione prima della riproduzione.
1. Crea un servizio di adesione locale su cui Primetime Cloud DRM eseguirà una query prima di consentire a qualsiasi dispositivo di riprodurre il contenuto che hai compilato.

Il servizio di adesione on-premise deve fornire una risposta a Primetime Cloud DRM che includa i due dati seguenti:

* `isAllowed`
* `drmPolicyToUse`

Questi determinano se un dispositivo può riprodurre il contenuto e quali criteri DRM utilizzare per generare la licenza DRM (se `isAllowed` è true).

Questo documento illustra le operazioni da eseguire per eseguire l&#39;opzione 2 di cui sopra: Implementa il tuo servizio di adesione esterna locale e rendilo disponibile a Primetime Cloud DRM per i contenuti che hai compilato.
