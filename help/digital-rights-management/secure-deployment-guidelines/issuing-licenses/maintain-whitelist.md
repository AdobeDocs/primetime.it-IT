---
description: Una whitelist è un elenco di entità affidabili.
seo-description: Una whitelist è un elenco di entità affidabili.
seo-title: Gestione di una whitelist di pacchetti di contenuti affidabili
title: Gestione di una whitelist di pacchetti di contenuti affidabili
uuid: 9a132ef9-eb56-408a-939e-1acd32d83a33
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Gestione di una whitelist di pacchetti di contenuti affidabili{#maintain-a-whitelist-of-trusted-content-packagers}

Una whitelist è un elenco di entità affidabili.

Per i pacchetti di contenuti, le entità sono organizzazioni considerate attendibili dal proprietario del contenuto per creare pacchetti (o cifrare) di file video e creare contenuto protetto DRM. Quando distribuite Adobe Primetime DRM, è necessario mantenere una whitelist di pacchetti di contenuti affidabili. Prima di rilasciare una licenza, è inoltre necessario verificare l&#39;identità di Content Packager nei metadati DRM di un file protetto DRM.

Per informazioni su come ottenere informazioni sull&#39;entità che crea il pacchetto del contenuto, consultate [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
