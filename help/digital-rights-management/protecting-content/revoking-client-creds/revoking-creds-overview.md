---
seo-title: Panoramica
title: Panoramica
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Overview{#overview}

Potrebbe essere necessario revocare le credenziali di un cliente o verificare se un determinato insieme di credenziali è già stato revocato a determinate condizioni. Le credenziali possono essere revocate se compromesse. Quando si verificano questi problemi, le licenze non vengono più rilasciate ai client compromessi.

 Adobe mantiene elenchi di revoca certificati (CRL) per la revoca di client compromessi. Tali CRL vengono applicati automaticamente dall&#39;SDK. I server delle licenze possono limitare ulteriormente i client impedendo particolari credenziali del computer o versioni particolari di DRM e credenziali runtime. È possibile creare un `RevocationList` e trasmetterlo nell&#39;SDK per revocare le credenziali del computer. È possibile revocare determinate versioni DRM/runtime sia a livello di criterio DRM impostando le restrizioni del modulo nel diritto di riproduzione che a livello globale impostando le restrizioni del modulo in `HandlerConfiguration`.

La discussione si concentra sulla revoca delle credenziali del client.
