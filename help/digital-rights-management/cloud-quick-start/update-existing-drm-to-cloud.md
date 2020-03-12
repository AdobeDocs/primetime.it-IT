---
seo-title: Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo)
title: Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo)
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo) {#update-existing-drm-content-to-use-cloud-drm-optional}

Se disponete di una libreria esistente di contenuto protetto da DRM di Primetime, è possibile &quot;ri-header&quot; il contenuto esistente per utilizzare il servizio DRM di Primetime Cloud, invece di dover reassemblare/cifrare i file sorgente originali. La riintestazione del contenuto aggiorna semplicemente i metadati DRM del contenuto nel manifesto HLS. Non esegue la decrittografia/ri-crittografia della risorsa originale. Questa può essere un&#39;opzione utile se il contenuto sorgente originale non è disponibile o se vi sono dubbi sulla quantità di risorse necessarie per creare nuovamente un pacchetto per una libreria di grandi dimensioni.

È possibile utilizzare Primetime DRM Java SDK per aggiornare i metadati a livello di programmazione. Inoltre, lo strumento della [!DNL OfflinePackager.jar] riga di comando incluso con questo kit di protezione può eseguire questo compito anche utilizzando l&#39; `-drm_refresh` opzione.

## Dettagli Di Nuova Intestazione {#section_3F3980D8E775450588C64E02A8448189}

Per utilizzare CloudDRM, è necessario aggiornare i campi seguenti:

* URL server licenze (Per [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificato server licenze (al certificato del server licenze CloudDRM)
* Certificato di trasporto (al certificato di trasporto CloudDRM)
* Credenziali Packager (alla credenziale packager attivata per l&#39;utilizzo con CloudDRM)

## Ricerca dei metadati DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

Il contenuto che utilizza la tecnologia HTTP (ad esempio HDS o HLS) utilizza un manifesto che fa riferimento ai metadati DRM di Adobe Access. In HDS, il `<drmmeta>` tag fa riferimento ai metadati; in HLS, il `#EXT-X-FAXS-CM` tag fa riferimento ai metadati. In entrambi i casi, i metadati possono essere contenuti in linea nel manifesto come BLOB codificati di base 64 o utilizzati come riferimento esterno come file binario. Se i metadati sono incorporati/agganciati nel manifesto, prima di utilizzare tali dati per creare un&#39;istanza dei metadati DRM potrebbe essere necessario decodificare i metadati in dati binari.

## Utilizzo di OfflinePackakger.jar incluso {#section_37C2091856E44AA380D742C72B4DD1A7}

Fornite il contenuto `-drm_refresh option` alla riga di comando. Verrà creato un nuovo file manifesto con i metadati DRM aggiornati, mentre il contenuto non verrà crittografato nuovamente.

## Utilizzo dell’SDK Java DRM di Primetime per rinominare la intestazione {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

Per aggiornare i metadati DRM esistenti è possibile utilizzare l&#39;SDK Java Primetime DRM (già noto come Adobe Access DRM) per un approccio programmatico. Per ulteriori dettagli, fai riferimento al [!DNL RegenerateMetadata.java] codice di esempio nel [!DNL /Reference Implmentation/Command Line Tools/samples/] pacchetto dell&#39;SDK. L’SDK Java di Adobe Access non fa parte di questo kit di protezione CloudDRM e deve essere acquisito direttamente da Adobe. Per ulteriori informazioni, contattate il vostro riferimento commerciale Adobe.