---
description: L’impostazione dei criteri consiste nel specificare le condizioni in base alle quali l’utente può riprodurre contenuti video protetti e quando e in che modo.
title: Impostazione dei criteri
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Impostazione dei criteri{#setting-policies}

L’impostazione dei criteri consiste nel specificare le condizioni in base alle quali l’utente può riprodurre contenuti video protetti e quando e in che modo.

La creazione dei criteri avviene come parte della richiesta del token di licenza. (vedere [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) ad esempio utilizzando Widevine).

Una volta che il codice lato server del cliente ha stabilito che rilascerà una licenza (in base a verifiche dei diritti, geolocalizzazione o qualsiasi altra informazione richiesta), richiede un token e *nel token* specifica il valore richiesto `securityLevel`, `hdcpOutputControl`, e `licenseDuration`. Queste sono le opzioni lato client per una policy Widevine. Altre soluzioni DRM offrono approcci simili, ma i dettagli sono diversi in ciascun caso e vengono elaborati nei singoli flussi di lavoro.

>[!NOTE]
>
>In Adobe viene fornito un server di riferimento di esempio che mostra come implementare un server di adesione/vetrina personalizzato: [Server di riferimento: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
