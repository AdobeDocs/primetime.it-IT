---
title: Revoca delle credenziali client
description: Revoca delle credenziali client
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Revoca delle credenziali client{#revoking-client-credentials}

A determinate condizioni è necessario revocare le credenziali di un cliente o verificare se un determinato insieme di credenziali è già stato revocato. Le credenziali possono essere revocate se sono compromesse. In questo caso, le licenze non verranno più rilasciate ai clienti compromessi.

Adobe gestisce elenchi di revoche di certificati (CRL, Certificate Revocation List) per la revoca di client compromessi. Questi CRL vengono applicati automaticamente dall’SDK. I server di licenza possono limitare ulteriormente i client impedendo particolari credenziali del computer o particolari versioni di DRM e credenziali di runtime. Per revocare le credenziali del computer, è possibile creare e trasmettere un elemento `RevocationList` nell’SDK. Particolari versioni DRM/runtime possono essere revocate a livello di criterio (impostando le restrizioni del modulo nel diritto di riproduzione) o globalmente (impostando le restrizioni del modulo nel `HandlerConfiguration`).

La discussione in questo capitolo sarà incentrata sulla revoca delle credenziali dei clienti.
