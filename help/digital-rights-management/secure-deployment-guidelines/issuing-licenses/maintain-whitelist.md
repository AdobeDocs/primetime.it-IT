---
description: Un elenco consentiti è un elenco di entità attendibili.
title: Gestisci un elenco consentiti di pacchetti di contenuti attendibili
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Gestisci un elenco consentiti di pacchetti di contenuti attendibili {#maintain-a-allowlist-of-trusted-content-packagers}

Un elenco consentiti è un elenco di entità attendibili.

Per i creatori di pacchetti di contenuti, le entità sono organizzazioni considerate attendibili dal proprietario del contenuto per creare pacchetti (o crittografare) di file video e creare contenuti protetti da DRM. Durante l’implementazione di Adobe Primetime DRM, è necessario mantenere un elenco consentiti di pacchetti di contenuti affidabili. Prima di rilasciare una licenza, è necessario verificare l&#39;identità del Content Packager nei metadati DRM di un file protetto da DRM.

Per informazioni su come ottenere informazioni sull’entità che ha creato il pacchetto del contenuto, consulta [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
