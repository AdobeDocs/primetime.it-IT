---
seo-title: Revoca delle credenziali client
title: Revoca delle credenziali client
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Revoca delle credenziali client{#revoking-client-credentials}

A determinate condizioni è necessario revocare le credenziali di un cliente o verificare se un determinato insieme di credenziali è già stato revocato. Le credenziali possono essere revocate se compromesse. In questo caso, le licenze non verranno più rilasciate ai client compromessi.

Adobe gestisce elenchi di revoca certificati (CRL) per la revoca di client compromessi. Tali CRL vengono applicati automaticamente dall&#39;SDK. I server delle licenze possono limitare ulteriormente i client impedendo particolari credenziali del computer o versioni particolari di DRM e credenziali runtime. Per revocare le credenziali del computer `RevocationList` può essere creato e passato nell’SDK. È possibile revocare determinate versioni DRM/runtime sia a livello di criterio (impostando le restrizioni del modulo nel diritto di riproduzione) che a livello globale (impostando le restrizioni del modulo nel `HandlerConfiguration`).

La discussione in questo capitolo sarà incentrata sulla revoca delle credenziali del client.
