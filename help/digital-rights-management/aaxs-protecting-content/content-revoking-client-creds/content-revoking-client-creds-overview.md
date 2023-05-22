---
title: Revoca delle credenziali del client
description: Revoca delle credenziali del client
copied-description: true
exl-id: 583dff28-c34a-4759-81a6-0471feab309f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Revoca delle credenziali del client{#revoking-client-credentials}

In determinate condizioni è necessario revocare le credenziali di un client o verificare se un determinato insieme di credenziali è già stato revocato. Le credenziali possono essere revocate se sono compromesse. In questo caso, le licenze non verranno più rilasciate ai client compromessi.

Adobe gestisce gli elenchi di revoche di certificati (CRL, Certificate Revocation List) per la revoca dei client compromessi. Questi CRL vengono applicati automaticamente dall’SDK. I server di licenze possono limitare ulteriormente i client disabilitando determinate credenziali del computer o particolari versioni di DRM e credenziali di runtime. A `RevocationList` possono essere create e passate nell&#39;SDK per revocare le credenziali del computer. È possibile revocare particolari versioni di DRM/runtime a livello di policy (impostando le restrizioni dei moduli nel diritto di riproduzione) o a livello globale (impostando le restrizioni dei moduli nel `HandlerConfiguration`).

La discussione in questo capitolo sarà incentrata sulla revoca delle credenziali del client.
