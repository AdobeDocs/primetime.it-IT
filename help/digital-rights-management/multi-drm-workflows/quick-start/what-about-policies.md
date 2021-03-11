---
description: L'impostazione dei criteri è il processo di specificazione delle condizioni per quando e come un utente può riprodurre contenuti video protetti.
title: Impostazione dei criteri
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Impostazione dei criteri{#setting-policies}

L&#39;impostazione dei criteri è il processo di specificazione delle condizioni per quando e come un utente può riprodurre contenuti video protetti.

La creazione dei criteri avviene come parte della richiesta del token di licenza. (Per un esempio che utilizza Widevine, consulta [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) .

Una volta che il codice lato server del cliente ha stabilito che rilascerà una licenza (in base ai controlli di idoneità, alla geolocalizzazione o a qualsiasi altra informazione richiesta), richiede un token e *nel token* specifica i `securityLevel`, `hdcpOutputControl` e `licenseDuration` richiesti. Queste sono le opzioni lato client per una politica Widevine. Altre soluzioni DRM offrono approcci simili, ma i dettagli sono diversi in ogni caso e sono elaborati nei singoli flussi di lavoro.

>[!NOTE]
>
>Adobe fornisce un esempio di server di riferimento che mostra come implementare il server di adesione o la vetrina: [Server di riferimento: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

