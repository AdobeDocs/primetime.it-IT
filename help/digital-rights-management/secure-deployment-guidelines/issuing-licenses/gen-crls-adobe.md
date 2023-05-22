---
description: È possibile utilizzare Adobe Primetime DRM per creare CRL che integrano il CRL del computer pubblicato da Adobe.
title: Generazione di CRL per integrare quelli pubblicati da Adobe
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Generazione di CRL per integrare quelli pubblicati da Adobe{#generating-crls-to-supplement-those-published-by-adobe}

È possibile utilizzare Adobe Primetime DRM per creare CRL che integrano il CRL del computer pubblicato da Adobe.

L’SDK di Primetime DRM verifica e applica i CRL Adobe. Tuttavia, è possibile non consentire l&#39;aggiunta di computer client creando un CRL che revoca le credenziali del computer aggiuntive passando il CRL all&#39;SDK DRM di Primetime. Quando rilasci una licenza, l’SDK controlla l’Adobe CRL e l’CRL.

Per generare i CRL, consulta [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
