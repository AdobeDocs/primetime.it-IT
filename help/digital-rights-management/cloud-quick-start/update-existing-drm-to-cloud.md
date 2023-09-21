---
title: Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo)
description: Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo) {#update-existing-drm-content-to-use-cloud-drm-optional}

Se disponi di una libreria di contenuti protetta da Primetime DRM, puoi rinominare l’intestazione dei contenuti esistenti per utilizzare il servizio Primetime Cloud DRM, invece di dover creare un nuovo pacchetto/crittografare i file di origine originali. La nuova intestazione del contenuto si limita ad aggiornare i metadati DRM del contenuto nel manifesto HLS. Non esegue operazioni di decrittografia o ricrittografia della risorsa originale. Questa può essere un’opzione utile se il contenuto sorgente originale non è disponibile o se si teme la quantità di risorse necessarie per creare nuovamente un pacchetto di una libreria di grandi dimensioni.

È possibile utilizzare l’SDK Java di Primetime DRM per aggiornare i metadati a livello di programmazione. Inoltre, la [!DNL OfflinePackager.jar] lo strumento da riga di comando incluso in questo kit di protezione può eseguire questa operazione utilizzando `-drm_refresh` opzione.

## Dettagli intestazione di nuovo {#section_3F3980D8E775450588C64E02A8448189}

Per utilizzare CloudDRM, il re-headering deve aggiornare i seguenti campi:

* URL server licenze (A [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificato server licenze (nel certificato server licenze CloudDRM)
* Certificato di trasporto (sul certificato di trasporto CloudDRM)
* Credenziali Packager (alle credenziali Packager attivate per l&#39;utilizzo con CloudDRM)

## Ricerca dei metadati DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

Il contenuto che utilizza la tecnologia HTTP (ad esempio HDS o HLS) utilizza un manifesto che fa riferimento ai metadati DRM di Access di Adobe. In HDS, i metadati sono referenziati da `<drmmeta>` e in HLS è indicato dal tag `#EXT-X-FAXS-CM` tag. In entrambi gli scenari, i metadati possono essere contenuti in linea nel manifesto come BLOB con codifica base 64 o essere referenziati esternamente come file binario. Se i metadati sono incorporati/in linea nel manifesto, potrebbe essere necessario prima decodificarli in base64 in dati binari prima di utilizzarli per creare istanze di metadati DRM.

## Utilizzo di OfflinePacakger.jar incluso {#section_37C2091856E44AA380D742C72B4DD1A7}

Fornire `-drm_refresh option` alla riga di comando. Verrà creato un nuovo file manifesto con i metadati DRM aggiornati, mentre il contenuto non verrà nuovamente crittografato.

## Utilizzo di Primetime DRM Java SDK per il re-header {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

L’aggiornamento di un metadati DRM esistente può essere eseguito utilizzando l’SDK Java di Primetime DRM (precedentemente noto come DRM di accesso Adobe) per un approccio programmatico. Per ulteriori informazioni, consultare [!DNL RegenerateMetadata.java] esempio di codice in [!DNL /Reference Implmentation/Command Line Tools/samples/] dell’SDK. L’SDK Java per l’accesso agli Adobi non fa parte di questo kit di protezione CloudDRM e deve essere acquisito direttamente da Adobe. Per ulteriori informazioni, contatta il contatto commerciale dell’Adobe.
