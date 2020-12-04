---
seo-title: Rilascio di licenze con binding di dominio
title: Rilascio di licenze con binding di dominio
uuid: 706650b7-6044-4c01-9f5a-90779127c9e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Rilascio di licenze con binding di dominio{#issuing-domain-bound-licenses}

Per rilasciare una licenza utilizzando un criterio DRM che richiede la registrazione del dominio, la richiesta del client deve includere un token di dominio valido emesso dal server di dominio specificato nel criterio. Quando il client richiede una licenza, include automaticamente i token di dominio per qualsiasi server di dominio specificato nei metadati di contenuto, a condizione che si sia registrato con tali server di dominio. Se il criterio DRM selezionato richiede la registrazione del dominio, l&#39;SDK seleziona automaticamente un token di dominio dalla richiesta per eseguire il binding della licenza o restituisce un errore se non è stato trovato alcun token di dominio appropriato.

Un token di dominio è considerato valido se non è scaduto e se è stato emesso da un CA di dominio autorizzato. Il server licenze deve specificare le autorità di dominio da cui accetta i token di dominio configurando `HandlerConfiguration.setDomainCAs()`. Se non è configurata alcuna CA di dominio, il server licenze non sarà in grado di rilasciare licenze associate a dominio.

Se i metadati includono più criteri DRM, la logica aziendale del server licenze potrebbe selezionare un criterio DRM basato sulla presentazione o meno da parte del client di un token di dominio. È possibile utilizzare `LicenseRequestMessage.getDomainTokens()` per determinare i domini con i quali il client si è registrato.
