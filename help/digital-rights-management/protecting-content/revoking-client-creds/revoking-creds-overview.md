---
seo-title: Panoramica
title: Panoramica
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Panoramica{#overview}

Potrebbe essere necessario revocare le credenziali di un cliente o verificare se un determinato insieme di credenziali è già stato revocato a determinate condizioni. Le credenziali possono essere revocate se compromesse. Quando si verificano questi problemi, le licenze non vengono più rilasciate ai client compromessi.

Adobe gestisce elenchi di revoca certificati (CRL) per la revoca di client compromessi. Tali CRL vengono applicati automaticamente dall&#39;SDK. I server delle licenze possono limitare ulteriormente i client impedendo particolari credenziali del computer o versioni particolari di DRM e credenziali runtime. Per revocare le credenziali del computer `RevocationList` può essere creato e passato nell’SDK. È possibile revocare determinate versioni DRM/runtime sia a livello di criterio DRM impostando le restrizioni del modulo nel diritto di riproduzione che a livello globale impostando le restrizioni del modulo in `HandlerConfiguration`.

La discussione si concentra sulla revoca delle credenziali del client.
