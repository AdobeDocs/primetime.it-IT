---
title: Panoramica sulle API
description: Panoramica sulle API
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Panoramica sulle API{#bees-overview}

È possibile implementare un servizio di titolarità back-end (BEES) per fornire una licenza personalizzata per l’operazione Primetime Cloud DRM.

Per impostazione predefinita, Primetime Cloud DRM utilizza la distribuzione anonima delle licenze. Ciò significa che tutte le richieste di licenza inviate a Primetime Cloud DRM restituiranno una licenza valida senza eseguire ulteriori controlli di autenticazione/autorizzazione (a meno che non sia stato applicato un vincolo di criterio che richiede l’utilizzo dell’autenticazione Adobe Primetime).

La richiesta di licenza contiene i criteri DRM utilizzati durante la creazione/crittografia del contenuto. Il criterio DRM viene utilizzato per generare la licenza DRM restituita al client. Nello scenario predefinito, è necessario prendere tutte le decisioni relative ai criteri DRM al momento della creazione del pacchetto di contenuti. I clienti che desiderano un controllo più preciso su questi flussi di lavoro possono scegliere tra le seguenti opzioni:

1. Integra l’autenticazione Primetime per aggiungere ulteriori controlli di adesione prima della riproduzione.
1. Creare un servizio di adesione on-premise su cui Primetime Cloud DRM eseguirà una query prima di consentire a qualsiasi dispositivo di riprodurre i contenuti inseriti nel pacchetto.

Il servizio di adesione on-premise deve fornire una risposta a Primetime Cloud DRM che includa i due dati seguenti:

* `isAllowed`
* `drmPolicyToUse`

Questi determinano se a un dispositivo è consentito riprodurre il contenuto e quali criteri DRM utilizzare per generare la licenza DRM (se `isAllowed` è true).

Questo documento descrive le operazioni da eseguire per eseguire l’opzione 2 di cui sopra: Implementa il servizio di adesione esterno on-premise e rendilo disponibile a Primetime Cloud DRM per i contenuti inseriti nel pacchetto.
