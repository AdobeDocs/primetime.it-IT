---
description: Un elenco di autorizzazioni è un elenco di entità affidabili.
seo-description: Un elenco di autorizzazioni è un elenco di entità affidabili.
seo-title: Gestisci un elenco di pacchetti di contenuti attendibili
title: Gestisci un elenco di pacchetti di contenuti attendibili
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Gestisci un elenco di pacchetti di contenuti affidabili{#maintain-a-allowlist-of-trusted-content-packagers}

Un elenco di autorizzazioni è un elenco di entità affidabili.

Per i pacchetti di contenuti, le entità sono organizzazioni considerate attendibili dal proprietario del contenuto per creare pacchetti (o cifrare) di file video e creare contenuto protetto DRM. Durante l&#39;implementazione di Adobe Primetime DRM, è necessario mantenere un elenco di pacchetti di contenuti affidabili. Prima di rilasciare una licenza, è inoltre necessario verificare l&#39;identità di Content Packager nei metadati DRM di un file protetto DRM.

Per informazioni su come ottenere informazioni sull&#39;entità che crea il pacchetto del contenuto, consultate [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
