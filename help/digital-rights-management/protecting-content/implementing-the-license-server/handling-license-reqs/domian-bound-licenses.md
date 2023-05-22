---
title: Rilascio di licenze a livello di dominio
description: Rilascio di licenze a livello di dominio
copied-description: true
exl-id: c29e61e5-d05a-4744-9ec8-7508ed814a57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Rilascio di licenze a livello di dominio{#issuing-domain-bound-licenses}

Per rilasciare una licenza utilizzando un criterio DRM che richiede la registrazione del dominio, la richiesta del client deve includere un token di dominio valido emesso dal server di dominio specificato nel criterio. Quando il client richiede una licenza, include automaticamente i token di dominio per qualsiasi server di dominio specificato nei metadati di contenuto, a condizione che sia stato registrato con tali server di dominio. Se il criterio DRM selezionato richiede la registrazione del dominio, l’SDK seleziona automaticamente un token di dominio dalla richiesta per associare la licenza a oppure restituisce un errore se non è stato trovato alcun token di dominio appropriato.

Un token di dominio è considerato valido se non è scaduto e se è stato rilasciato da una CA di dominio autorizzata. Il server licenze deve specificare le autorità di dominio da cui accetta i token di dominio configurando `HandlerConfiguration.setDomainCAs()`. Se non è configurata alcuna CA di dominio, il server licenze non sarà in grado di rilasciare licenze a livello di dominio.

Se i metadati includono più criteri DRM, la logica di business del server licenze potrebbe selezionare un criterio DRM basato sulla presentazione di un token di dominio da parte del client. È possibile utilizzare `LicenseRequestMessage.getDomainTokens()` per determinare i domini con cui il client si è registrato.
