---
title: Aggiorna il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo)
description: Aggiorna il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---


# Aggiornare il contenuto DRM esistente per utilizzare Cloud DRM (facoltativo) {#update-existing-drm-content-to-use-cloud-drm-optional}

Se disponi di una libreria di contenuti esistente protetta da DRM di Primetime, è possibile &quot;ri-header&quot; il contenuto esistente per utilizzare il servizio DRM di Primetime Cloud, invece di dover reassemblare/crittografare i file sorgente originali. La riintestazione del contenuto aggiorna semplicemente i metadati DRM del contenuto nel manifesto HLS. Non esegue la decrittografia/ri-crittografia della risorsa originale. Questa opzione può essere utile se il contenuto sorgente originale non è disponibile o se vi sono dubbi sulla quantità di risorse necessarie per creare nuovamente un pacchetto per una libreria di grandi dimensioni.

È possibile utilizzare l’SDK Java DRM di Primetime per aggiornare i metadati a livello di programmazione. Inoltre, lo strumento della riga di comando [!DNL OfflinePackager.jar] incluso con questo kit di protezione può eseguire questo compito anche utilizzando l&#39;opzione `-drm_refresh`.

## Dettagli di nuova intestazione {#section_3F3980D8E775450588C64E02A8448189}

Per utilizzare CloudDRM, è necessario aggiornare i campi seguenti:

* URL del server licenze (a [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Certificato del server licenze (al certificato del server licenze CloudDRM)
* Certificato di trasporto (al certificato di trasporto CloudDRM)
* Credenziale Packager (alla credenziale del packager attivata per l&#39;utilizzo con CloudDRM)

## Ricerca dei metadati DRM {#section_28721CB7966F40708AEC8637F2E9BB72}

I contenuti che utilizzano la tecnologia HTTP (come HDS o HLS) utilizzano un manifesto che fa riferimento ai metadati DRM di accesso Adobe. In HDS, i metadati sono referenziati dal tag `<drmmeta>` e in HLS, è referenziato dal tag `#EXT-X-FAXS-CM` . In entrambi i casi, i metadati possono essere contenuti in linea nel manifesto come un BLOB codificato base-64, o referenziati esternamente come file binario. Se i metadati sono incorporati/in linea nel manifesto, potrebbe essere necessario prima decodificare i metadati di base64 in dati binari prima di utilizzare tali dati per creare un&#39;istanza dei metadati DRM.

## Utilizzo di OfflinePacger.jar incluso {#section_37C2091856E44AA380D742C72B4DD1A7}

Fornisci il `-drm_refresh option` alla riga di comando. Verrà creato un nuovo file manifesto con metadati DRM aggiornati, mentre il contenuto non verrà ri-crittografato.

## Utilizzo dell&#39;SDK Java DRM di Primetime per la nuova intestazione {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

L’aggiornamento di un metadati DRM esistente può essere eseguito utilizzando l’SDK Java Primetime DRM (precedentemente noto come DRM di accesso Adobe) per un approccio programmatico. Per ulteriori dettagli, fai riferimento al codice di esempio [!DNL RegenerateMetadata.java] nel pacchetto [!DNL /Reference Implmentation/Command Line Tools/samples/] dell&#39;SDK. L’SDK Java per l’accesso agli Adobi non fa parte di questo kit di protezione CloudDRM e deve essere acquisito direttamente dall’Adobe. Per ulteriori informazioni, contatta il tuo contatto commerciale Adobe.