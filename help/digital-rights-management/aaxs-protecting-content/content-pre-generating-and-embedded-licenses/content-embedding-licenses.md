---
title: Incorporazione di licenze
description: Incorporazione di licenze
copied-description: true
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Incorporazione di licenze {#embedding-licenses}

Una volta che il contenuto è stato crittografato e una licenza è stata pregenerata, la licenza può essere incorporata nel contenuto crittografato.

Per incorporare una licenza, ottieni un’istanza di `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se conosci il tipo di contenuto crittografato, utilizza il costruttore per `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; in caso contrario, utilizzare `MediaProcessorFactory.getMediaProcessor()` per restituire un&#39;istanza in base al tipo di file rilevato. Costruire un `KeyMetaDataCallback` e richiamare `modifyKeyMetaData()`. L’implementazione del callback verrà richiamata quando i metadati DRM si trovano nel contenuto crittografato. In base ai metadati trovati, puoi scegliere una licenza da incorporare e impostare la licenza utilizzando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Per un codice di esempio che illustra le licenze incorporate, consulta `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` nella directory &quot;Samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.

>[!NOTE]
>
>I client di Adobe Access 2.0 ignoreranno tutte le licenze incorporate nel contenuto e tenteranno di ottenere una licenza dal server licenze specificato nei metadati. Tuttavia, se i metadati indicano che non è disponibile alcun server licenze, sarà necessario aggiornare un client di Access 2.0 di Adobe per visualizzare il contenuto.

Consulta [Licenze out-of-band](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
