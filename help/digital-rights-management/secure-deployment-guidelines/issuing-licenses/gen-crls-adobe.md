---
description: È possibile utilizzare  Adobe Primetime DRM per creare CRL che integrano il computer CRL pubblicato da  Adobe.
seo-description: È possibile utilizzare  Adobe Primetime DRM per creare CRL che integrano il computer CRL pubblicato da  Adobe.
seo-title: 'Generazione di CRL per completare quelli pubblicati dal Adobe '
title: 'Generazione di CRL per completare quelli pubblicati dal Adobe '
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Generazione di CRL per completare quelli pubblicati da  Adobe{#generating-crls-to-supplement-those-published-by-adobe}

È possibile utilizzare  Adobe Primetime DRM per creare CRL che integrano il computer CRL pubblicato da  Adobe.

L&#39;SDK DRM di Primetime verifica e applica i CRL del Adobe . Tuttavia, è possibile rifiutare computer client aggiuntivi creando un CRL che revoca credenziali computer aggiuntive trasmettendo il CRL all&#39;SDK DRM di Primetime. Quando rilasci una licenza, l&#39;SDK verifica il CRL del Adobe  e il CRL.

Per generare CRL, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
