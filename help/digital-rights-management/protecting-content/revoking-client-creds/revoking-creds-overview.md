---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Panoramica{#overview}

Potrebbe essere necessario revocare le credenziali di un cliente o verificare se un determinato insieme di credenziali è già stato revocato in determinate condizioni. Le credenziali possono essere revocate se compromesse. Quando si verificano questi problemi, le licenze non vengono più rilasciate ai clienti compromessi.

Adobe gestisce elenchi di revoche di certificati (CRL, Certificate Revocation List) per la revoca di client compromessi. Questi CRL vengono applicati automaticamente dall’SDK. I server di licenza possono limitare ulteriormente i client impedendo particolari credenziali del computer o particolari versioni di DRM e credenziali di runtime. Per revocare le credenziali del computer, è possibile creare e trasmettere un elemento `RevocationList` nell’SDK. Le particolari versioni DRM/runtime possono essere revocate a livello di criterio DRM impostando le restrizioni del modulo nel diritto di riproduzione o globalmente impostando le restrizioni del modulo nel `HandlerConfiguration`.

La discussione si concentra sulla revoca delle credenziali del cliente.
