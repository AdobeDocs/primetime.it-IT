---
description: Per utilizzare elenchi di revoche di certificati (CRL, Certificate Revocation List) generati localmente ed elenchi di aggiornamenti di criteri, utilizzate le API DRM di Adobe Primetime per verificare la firma.
seo-description: Per utilizzare elenchi di revoche di certificati (CRL, Certificate Revocation List) generati localmente ed elenchi di aggiornamenti di criteri, utilizzate le API DRM di Adobe Primetime per verificare la firma.
seo-title: Utilizzo di CRL generati localmente
title: Utilizzo di CRL generati localmente
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Utilizzo di CRL generati localmente {#consuming-locally-generated-crls}

Per utilizzare elenchi di revoche di certificati (CRL, Certificate Revocation List) generati localmente ed elenchi di aggiornamenti di criteri, utilizzate le API DRM di Adobe Primetime per verificare la firma.

Le seguenti API verificano che gli elenchi non siano stati alterati e che gli elenchi siano stati firmati dal server licenze corretto:

* Chiamare [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) per verificare la firma prima di fornire [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualsiasi API.

   Per ulteriori informazioni, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chiama [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) per controllare la firma prima di fornire l&#39;API `PolicyUpdateList` a qualsiasi API.

   Per ulteriori informazioni, vedere [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

