---
description: L'impostazione dei criteri è il processo che consente di specificare le condizioni per la riproduzione di contenuto video protetto da parte dell'utente.
seo-description: L'impostazione dei criteri è il processo che consente di specificare le condizioni per la riproduzione di contenuto video protetto da parte dell'utente.
seo-title: Impostazione dei criteri
title: Impostazione dei criteri
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Impostazione criteri{#setting-policies}

L&#39;impostazione dei criteri è il processo che consente di specificare le condizioni per la riproduzione di contenuto video protetto da parte dell&#39;utente.

La creazione dei criteri avviene come parte della richiesta di token di licenza. (vedere [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) per un esempio che utilizza Widevine).

Una volta determinato che il codice lato server del cliente rilascerà una licenza (in base a controlli di adesione, geolocalizzazione o qualsiasi altra informazione richiesta), il cliente richiede un token e *nel token* specifica i `securityLevel`, `hdcpOutputControl` e `licenseDuration` richiesti. Queste sono le opzioni lato client per un criterio Widevine. Altre soluzioni DRM offrono approcci simili, ma i dettagli sono diversi in ogni caso, e sono elaborati nei singoli flussi di lavoro.

>[!NOTE]
>
> Adobe fornisce un server di riferimento di esempio che mostra come implementare un proprio server di adesione / storefront: [Server di riferimento: Esempio di ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

