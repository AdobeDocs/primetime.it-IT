---
seo-title: INFORMAZIONI SULLE API
title: INFORMAZIONI SULLE API
uuid: c6ee7528-fdfa-4a56-bea2-a5e2dab6d428
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# INFORMAZIONI SULLE API{#bees-overview}

Potete implementare un servizio di adesione back-end (BEES) per fornire l&#39;adesione personalizzata per l&#39;operazione DRM di Primetime Cloud.

Primetime Cloud DRM utilizza per impostazione predefinita una licenza anonima. Ciò significa che tutte le richieste di licenza inviate a Primetime Cloud DRM restituiranno una licenza valida senza eseguire ulteriori controlli di autenticazione/autorizzazione (a meno che non sia stato applicato un vincolo di criterio che richiede l&#39;utilizzo dell&#39;autenticazione Adobe Primetime).

La richiesta di licenza contiene il criterio DRM utilizzato durante la creazione del pacchetto/crittografia del contenuto. Il criterio DRM viene utilizzato per generare la licenza DRM restituita al client. Nello scenario predefinito, è necessario prendere tutte le decisioni relative ai criteri DRM al momento della creazione del contenuto. I clienti che desiderano un maggiore controllo su questi flussi di lavoro possono scegliere tra le seguenti opzioni:

1. Integrate l&#39;autenticazione Primetime per aggiungere ulteriori controlli di adesione prima della riproduzione.
1. Create un servizio di adesione locale al quale Primetime Cloud DRM eseguirà una query prima di consentire a qualsiasi dispositivo di riprodurre il contenuto creato in un pacchetto.

Il servizio di adesione locale deve fornire una risposta a Primetime Cloud DRM che include i due dati seguenti:

* `isAllowed`
* `drmPolicyToUse`

Questi determinano se un dispositivo può riprodurre il contenuto e quale criterio DRM utilizzare per generare la licenza DRM (se `isAllowed` è vero).

Questo documento illustra le operazioni necessarie per eseguire l&#39;opzione 2: Implementate il vostro servizio di adesione esterna locale e renderlo disponibile a Primetime Cloud DRM per i contenuti inclusi nel pacchetto.
