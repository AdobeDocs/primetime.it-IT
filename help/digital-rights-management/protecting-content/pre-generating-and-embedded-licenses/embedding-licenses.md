---
title: Incorporazione di licenze
description: Incorporazione di licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Incorporazione di licenze {#embedding-licenses}

Una volta crittografato il contenuto e pregenerata una licenza, la licenza può essere incorporata nel contenuto crittografato.

Se desideri incorporare una licenza, devi ottenere un’istanza di `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se si conosce il tipo di contenuto crittografato, utilizzare il costruttore per `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; in caso contrario, utilizza `MediaProcessorFactory.getMediaProcessor()` per restituire un’istanza in base al tipo di file rilevato. Quindi devi costruire un `KeyMetaDataCallback` e richiamare `modifyKeyMetaData()`. L’implementazione di callback viene quindi richiamata quando i metadati DRM si trovano nel contenuto crittografato. In base ai metadati trovati, puoi scegliere una licenza da incorporare e impostare la licenza utilizzando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulta `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` nella directory Strumenti della riga di comando per l’implementazione di riferimento [!DNL Samples] per un esempio di codice che illustra le licenze incorporate.

>[!NOTE]
>
>Un client Adobe Primetime DRM 2.0 ignora tutte le licenze incorporate nel contenuto e tenta di ottenere una licenza dal server licenze specificato nei metadati. Tuttavia, se i metadati indicano che non è disponibile alcun server licenze, è necessario aggiornare un client Primetime DRM 2.0 prima di poter visualizzare il contenuto.

