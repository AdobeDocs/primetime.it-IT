---
description: Per utilizzare gli elenchi di revoche di certificati (CRL) generati localmente e gli elenchi di aggiornamento dei criteri, utilizza le API Adobe Primetime DRM per verificare la firma.
title: Utilizzo di CRL generati localmente
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Utilizzo di CRL generati localmente {#consuming-locally-generated-crls}

Per utilizzare gli elenchi di revoche di certificati (CRL) generati localmente e gli elenchi di aggiornamento dei criteri, utilizza le API Adobe Primetime DRM per verificare la firma.

Le seguenti API verificano che gli elenchi non siano stati manomessi e che siano stati firmati dal server licenze corretto:

* Chiamata [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) per verificare la firma prima di fornire [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualsiasi API.

   Per ulteriori informazioni, consulta [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chiamata [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) per verificare la firma prima di fornire `PolicyUpdateList` a qualsiasi API.

   Per ulteriori informazioni, consulta [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

