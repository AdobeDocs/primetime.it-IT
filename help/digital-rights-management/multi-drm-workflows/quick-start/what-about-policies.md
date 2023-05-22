---
description: L’impostazione dei criteri consiste nel specificare le condizioni in base alle quali l’utente può riprodurre contenuti video protetti e quando e in che modo.
title: Impostazione dei criteri
exl-id: ab7295c8-88f2-4d4a-a7f1-3332df7bb735
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
