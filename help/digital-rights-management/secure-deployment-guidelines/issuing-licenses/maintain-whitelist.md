---
description: Un elenco consentiti è un elenco di entità affidabili.
title: Gestisci un elenco consentiti di pacchetti di contenuti affidabili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Gestisci un elenco consentiti di pacchetti di contenuti affidabili {#maintain-a-allowlist-of-trusted-content-packagers}

Un elenco consentiti è un elenco di entità affidabili.

Per i pacchetti di contenuti, le entità sono organizzazioni affidabili dal proprietario del contenuto per creare pacchetti (o cifrare) dei file video e creare contenuti protetti da DRM. Quando distribuisci Adobe Primetime DRM, devi mantenere un elenco consentiti di pacchetti di contenuti affidabili. È inoltre necessario verificare l&#39;identità del content packager nei metadati DRM di un file protetto DRM prima di rilasciare una licenza.

Per informazioni su come ottenere informazioni sull&#39;entità che ha generato il contenuto, consulta [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).
