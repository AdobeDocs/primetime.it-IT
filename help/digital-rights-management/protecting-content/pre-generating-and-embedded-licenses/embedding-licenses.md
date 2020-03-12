---
seo-title: Incorporazione di licenze
title: Incorporazione di licenze
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Incorporazione di licenze {#embedding-licenses}

Una volta crittografato il contenuto e pregenerata una licenza, la licenza può essere incorporata nel contenuto crittografato.

Se si desidera incorporare una licenza, è necessario ottenere un&#39;istanza di `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se si conosce il tipo di contenuto crittografato, utilizzare il costruttore per `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; in caso contrario, utilizzare `MediaProcessorFactory.getMediaProcessor()` per restituire un&#39;istanza in base al tipo di file rilevato. Quindi devi costruire un `KeyMetaDataCallback` e invocare `modifyKeyMetaData()`. L&#39;implementazione di callback viene quindi richiamata quando i metadati DRM si trovano nel contenuto crittografato. In base ai metadati trovati, potete scegliere una licenza da incorporare e impostare la licenza utilizzando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Per un esempio di codice che illustra le licenze incorporate, vedere `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` nella directory Strumenti della riga di comando Implementazione di riferimento [!DNL Samples] .

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Un client Adobe Primetime DRM 2.0 ignora tutte le licenze incorporate nel contenuto, quindi tenta di ottenere una licenza dal server licenze specificata nei metadati. Tuttavia, se i metadati indicano che non è disponibile alcun server licenze, è necessario aggiornare un client Primetime DRM 2.0 prima di poter visualizzare il contenuto.

