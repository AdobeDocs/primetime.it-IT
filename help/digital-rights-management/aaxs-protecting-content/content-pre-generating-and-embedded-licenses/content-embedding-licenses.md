---
seo-title: Incorporazione di licenze
title: Incorporazione di licenze
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Incorporazione di licenze {#embedding-licenses}

Una volta crittografato il contenuto e pregenerata una licenza, la licenza può essere incorporata nel contenuto crittografato.

Per incorporare una licenza, ottenere un&#39;istanza di `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se si conosce il tipo di contenuto crittografato, utilizzare il costruttore per `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; in caso contrario, utilizzare `MediaProcessorFactory.getMediaProcessor()` per restituire un&#39;istanza in base al tipo di file rilevato. Crea un `KeyMetaDataCallback` e invoca `modifyKeyMetaData()`. L&#39;implementazione di callback verrà richiamata quando i metadati DRM si trovano nel contenuto crittografato. In base ai metadati trovati, potete scegliere una licenza da incorporare e impostare la licenza utilizzando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Per un esempio di codice che illustra le licenze incorporate, vedere `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` nella directory &quot;Samples&quot; degli strumenti della riga di comando Implementazione di riferimento.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>I client Adobe Access 2.0 ignoreranno tutte le licenze incorporate nel contenuto e cercheranno di ottenere una licenza dal server licenze specificato nei metadati. Tuttavia, se i metadati indicano che non è disponibile alcun server licenze, per visualizzare il contenuto sarà necessario aggiornare un client Adobe Access 2.0.

Consultate Licenze [fuori banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
