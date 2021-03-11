---
title: Rilascio di licenze con associazione a dominio
description: Rilascio di licenze con associazione a dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Rilascio di licenze associate a domini{#issuing-domain-bound-licenses}

Per emettere una licenza utilizzando un criterio DRM che richiede la registrazione del dominio, la richiesta del client deve includere un token di dominio valido emesso dal server di dominio specificato nel criterio. Quando il client richiede una licenza, include automaticamente i token di dominio per qualsiasi server di dominio specificato nei metadati di contenuto, a condizione che sia registrato con tali server di dominio. Se il criterio DRM selezionato richiede la registrazione del dominio, l&#39;SDK seleziona automaticamente un token di dominio dalla richiesta per eseguire il binding della licenza o restituisce un errore se non è stato trovato alcun token di dominio appropriato.

Un token di dominio è considerato valido se non è scaduto e se è stato rilasciato da una CA di dominio autorizzata. Il server licenze deve specificare le autorità di dominio da cui accetta i token di dominio configurando `HandlerConfiguration.setDomainCAs()`. Se non sono configurate CA di dominio, il server licenze non sarà in grado di rilasciare licenze associate a dominio.

Se i metadati includono più criteri DRM, la logica aziendale del server licenze potrebbe selezionare un criterio DRM basato sulla presentazione o meno di un token di dominio da parte del client. Puoi utilizzare `LicenseRequestMessage.getDomainTokens()` per determinare i domini con cui il client si è registrato.
