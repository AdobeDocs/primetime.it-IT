---
title: Incorporazione di licenze
description: Incorporazione di licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Incorporazione di licenze {#embedding-licenses}

Una volta che il contenuto è stato crittografato e una licenza è stata pregenerata, la licenza può essere incorporata nel contenuto crittografato.

Se desideri incorporare una licenza, devi ottenere un’istanza di `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se conosci il tipo di contenuto crittografato, utilizza il costruttore per `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; in caso contrario, utilizzare `MediaProcessorFactory.getMediaProcessor()` per restituire un&#39;istanza in base al tipo di file rilevato. Quindi è necessario costruire un `KeyMetaDataCallback` e richiamare `modifyKeyMetaData()`. L’implementazione del callback viene quindi richiamata quando i metadati DRM si trovano nel contenuto crittografato. In base ai metadati trovati, puoi scegliere una licenza da incorporare e impostare la licenza utilizzando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulta `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` negli strumenti della riga di comando per l’implementazione di riferimento [!DNL Samples] per il codice di esempio che illustra le licenze incorporate.

>[!NOTE]
>
>Un client Adobe Primetime DRM 2.0 ignora le licenze incorporate nel contenuto e quindi tenta di ottenere una licenza dal server licenze specificata nei metadati. Tuttavia, se i metadati indicano che non è disponibile alcun server licenze, è necessario aggiornare un client Primetime DRM 2.0 prima di poter visualizzare il contenuto.
