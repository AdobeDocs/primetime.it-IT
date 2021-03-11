---
description: Per utilizzare elenchi di revoche di certificati (CRL) generati localmente e elenchi di aggiornamenti dei criteri, utilizza le API DRM di Adobe Primetime per verificare la firma.
title: Utilizzo di CRL generati localmente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Utilizzo di CRL generati localmente {#consuming-locally-generated-crls}

Per utilizzare elenchi di revoche di certificati (CRL) generati localmente e elenchi di aggiornamenti dei criteri, utilizza le API DRM di Adobe Primetime per verificare la firma.

Le seguenti API verificano che gli elenchi non siano stati manomessi e che siano stati firmati dal server licenze corretto:

* Chiama [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) per controllare la firma prima di fornire il [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualsiasi API.

   Per ulteriori informazioni, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chiama [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) per controllare la firma prima di fornire `PolicyUpdateList` a qualsiasi API.

   Per ulteriori informazioni, vedere [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

