---
description: È possibile utilizzare Adobe Primetime DRM per creare CRL che integrano il machine CRL pubblicato da Adobe.
title: Generazione di CRL per integrare quelli pubblicati dall’Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Generazione di CRL per completare quelli pubblicati da Adobe{#generating-crls-to-supplement-those-published-by-adobe}

È possibile utilizzare Adobe Primetime DRM per creare CRL che integrano il machine CRL pubblicato da Adobe.

L’SDK DRM di Primetime controlla e applica gli Adobe CRL. Tuttavia, puoi impedire l’utilizzo di computer client aggiuntivi creando un CRL che revoca le credenziali aggiuntive del computer passando il CRL all’SDK DRM di Primetime. Quando rilasci una licenza, l&#39;SDK controlla l&#39;Adobe CRL e il tuo CRL.

Per generare CRL, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
