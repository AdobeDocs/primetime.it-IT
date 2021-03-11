---
title: Rilascio di licenze con associazione a dominio
description: Rilascio di licenze con associazione a dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Rilascio di licenze legate a dominio{#issuing-domain-bound-licenses}

Per rilasciare una licenza utilizzando un criterio che richiede la registrazione del dominio, la richiesta del client deve includere un token di dominio valido emesso dal server di dominio specificato nel criterio. Quando il client richiede una licenza, include automaticamente i token di dominio per qualsiasi server di dominio specificato nei metadati del contenuto, se si è registrato con tali server di dominio. Se il criterio selezionato richiede la registrazione del dominio, l’SDK selezionerà automaticamente un token di dominio dalla richiesta per eseguire il binding della licenza a o restituirà un errore se non è stato trovato alcun token di dominio appropriato.

Un token di dominio è considerato valido se non è scaduto e se è stato rilasciato da una CA di dominio autorizzata. Il server licenze deve specificare le autorità di dominio da cui accetta i token di dominio configurando `HandlerConfiguration.setDomainCAs()`. Se non sono configurate CA di dominio, il server licenze non sarà in grado di rilasciare licenze associate a dominio.

Se i metadati includono più criteri, la logica di business del server licenze potrebbe selezionare un criterio in base al fatto che il client abbia presentato o meno un token di dominio. Utilizza `LicenseRequestMessage.getDomainTokens()` per determinare i domini con cui il client si è registrato.
