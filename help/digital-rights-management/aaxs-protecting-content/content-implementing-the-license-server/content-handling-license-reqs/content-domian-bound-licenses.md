---
seo-title: Rilascio di licenze con associazione a dominio
title: Rilascio di licenze con associazione a dominio
uuid: 175d3b7d-d1df-44ee-85ad-a0db4a1bdb9d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Rilascio di licenze con associazione a dominio{#issuing-domain-bound-licenses}

Per rilasciare una licenza utilizzando un criterio che richiede la registrazione del dominio, la richiesta del client deve includere un token di dominio valido emesso dal server di dominio specificato nel criterio. Quando il client richiede una licenza, includerà automaticamente i token di dominio per qualsiasi server di dominio specificato nei metadati di contenuto, se si è registrato con tali server di dominio. Se il criterio selezionato richiede la registrazione del dominio, l&#39;SDK selezionerà automaticamente un token di dominio dalla richiesta per il binding della licenza, oppure restituirà un errore se non è stato trovato alcun token di dominio appropriato.

Un token di dominio è considerato valido se non è scaduto e se è stato emesso da un CA di dominio autorizzato. Il server licenze deve specificare le autorità di dominio da cui accetta i token di dominio configurando `HandlerConfiguration.setDomainCAs()`. Se non è configurata alcuna CA di dominio, il server licenze non sarà in grado di rilasciare licenze associate a dominio.

Se i metadati includono più criteri, la logica aziendale del server licenze potrebbe selezionare un criterio in base al fatto che il client abbia presentato o meno un token di dominio. Utilizzare `LicenseRequestMessage.getDomainTokens()` per determinare i domini con i quali il client si è registrato.
