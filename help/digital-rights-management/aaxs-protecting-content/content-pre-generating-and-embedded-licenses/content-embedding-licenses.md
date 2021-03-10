---
title: Incorporazione di licenze
description: Incorporazione di licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Incorporazione di licenze {#embedding-licenses}

Una volta crittografato il contenuto e pregenerata una licenza, la licenza può essere incorporata nel contenuto crittografato.

Per incorporare una licenza, ottenere un&#39;istanza di `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se si conosce il tipo di contenuto crittografato, utilizzare il costruttore per `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; in caso contrario, utilizza `MediaProcessorFactory.getMediaProcessor()` per restituire un’istanza in base al tipo di file rilevato. Costruire un `KeyMetaDataCallback` e richiamare `modifyKeyMetaData()`. L’implementazione di callback verrà richiamata quando i metadati DRM si trovano nel contenuto crittografato. In base ai metadati trovati, puoi scegliere una licenza da incorporare e impostare la licenza utilizzando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Per un esempio di codice che illustra le licenze incorporate, vedi `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` nella directory &quot;Samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.

>[!NOTE]
>
>I client di Adobe Access 2.0 ignoreranno tutte le licenze incorporate nel contenuto e cercheranno di ottenere una licenza dal server licenze specificato nei metadati. Tuttavia, se i metadati indicano che non è disponibile alcun server licenze, per visualizzare il contenuto sarà necessario un client Adobe Access 2.0.

Consulta [Licenze fuori banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
