---
title: Rilascio di licenze a livello di dominio
description: Rilascio di licenze a livello di dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Rilascio di licenze a livello di dominio{#issuing-domain-bound-licenses}

Per rilasciare una licenza utilizzando un criterio che richiede la registrazione del dominio, la richiesta del client deve includere un token di dominio valido emesso dal server di dominio specificato nel criterio. Quando il client richiede una licenza, includerà automaticamente i token di dominio per qualsiasi server di dominio specificato nei metadati del contenuto, se è stato registrato con tali server di dominio. Se il criterio selezionato richiede la registrazione del dominio, l’SDK seleziona automaticamente un token di dominio dalla richiesta a cui associare la licenza oppure, se non è stato trovato alcun token di dominio appropriato, restituisce un errore.

Un token di dominio è considerato valido se non è scaduto e se è stato rilasciato da una CA di dominio autorizzata. Il server licenze deve specificare le autorità di dominio da cui accetta i token di dominio configurando `HandlerConfiguration.setDomainCAs()`. Se non è configurata alcuna CA di dominio, il server licenze non sarà in grado di rilasciare licenze a livello di dominio.

Se i metadati includono più criteri, la regola business del server licenze potrebbe selezionare un criterio in base al fatto che il client abbia presentato un token di dominio. Utilizzare `LicenseRequestMessage.getDomainTokens()` per determinare i domini con cui il client si è registrato.
