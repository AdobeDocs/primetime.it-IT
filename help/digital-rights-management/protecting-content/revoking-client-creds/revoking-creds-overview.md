---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 332343ce-ac22-41a5-801a-3597476f0eaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Panoramica{#overview}

Potrebbe essere necessario revocare le credenziali di un client o verificare se un determinato set di credenziali è già stato revocato in determinate condizioni. Le credenziali possono essere revocate se sono compromesse. Quando si verificano questi problemi, le licenze non vengono più rilasciate ai client compromessi.

Adobe gestisce gli elenchi di revoche di certificati (CRL, Certificate Revocation List) per la revoca dei client compromessi. Questi CRL vengono applicati automaticamente dall’SDK. I server di licenze possono limitare ulteriormente i client disabilitando determinate credenziali del computer o particolari versioni di DRM e credenziali di runtime. A `RevocationList` possono essere create e passate nell&#39;SDK per revocare le credenziali del computer. È possibile revocare particolari versioni DRM/runtime a livello di policy DRM impostando le restrizioni del modulo nel diritto di riproduzione o a livello globale impostando le restrizioni del modulo nel `HandlerConfiguration`.

La discussione è incentrata sulla revoca delle credenziali del client.
