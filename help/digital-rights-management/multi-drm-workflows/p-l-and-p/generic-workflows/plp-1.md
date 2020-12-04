---
description: Potete utilizzare  Adobe  packager offline per preparare il contenuto per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.
seo-description: Potete utilizzare  Adobe  packager offline per preparare il contenuto per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.
seo-title: Primetime Packager / Cloud DRM / TVSDK
title: Primetime Packager / Cloud DRM / TVSDK
uuid: e54a0e4d-c8ea-46d4-b1b0-bed8a680f8f5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Primetime Packager / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

Potete utilizzare  Adobe  packager offline per preparare il contenuto per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.

Questa serie di istruzioni presuppone che sia già stato configurato un account amministratore ExpressPlay: [Primetime DRM Cloud Quick-start](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Scegliete l&#39;infrastruttura da utilizzare per creare il pacchetto dei contenuti. Primetime Packager supporta sia la creazione di pacchetti di contenuti da riga di comando che basati sulla configurazione da utilizzare con i DRM FairPlay, Widevine e PlayReady. I seguenti formati e la seguente crittografia sono attualmente supportati in TVSDK (con altre informazioni nella pipeline):

   * DASH (CENC) / PlayReady, Widevine - Per HTML5
   * HLS / FairPlay, Accesso - Per iOS

1. Scegliere un sistema di gestione delle chiavi (KMS):

   * utilizzare il KMS ExpressPlay ( [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/)); questo sistema gestisce le chiavi di contenuto tramite l&#39;API RESTful di ExpressPlay.

      o...

   * Configurate il vostro KMS. Create un database di chiavi di contenuto selezionabile da Content-ID.

      In entrambi i casi, KMS gestisce una serie di chiavi di contenuto, con ciascuna chiave associata a un Content-ID.

1. Create pacchetti per il contenuto. Con Primetime Packager, potete creare pacchetti di contenuto per una soluzione DRM specifica o per più soluzioni DRM.

   I seguenti comandi di esempio mostrano alcuni esempi di creazione di pacchetti di contenuto per diverse soluzioni DRM:

   * [Widevine con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19)  (genera il file MPD):

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [FairPlay con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (genera un file M3U8):

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >Il valore `key_url` viene copiato come nel file M3U8.

1. Creare un &quot;server storefront&quot;.

       Il server storefront deve gestire le seguenti operazioni:
   
   1. Selezione del contenuto da parte del cliente. Questa implementazione deve includere un endpoint per i client per richiedere un token contenuto per un ID contenuto specifico.
   1. Adesione cliente
   1. Richieste di token di licenza (ExpressPlay) dal client ( [Richiesta token di licenza ExpressPlay / riferimento risposta](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Crea il tuo client.

       Il client deve includere una chiamata al server di storefront.  Adobe consiglia al client di chiamare lo storefront dopo che l&#39;utente ha selezionato del contenuto e dopo che l&#39;utente è stato autenticato. Quindi, passare il token restituito da ExpressPlay al lettore per utilizzarlo per le richieste di licenza. Le presentazioni per l&#39;implementazione del componente DRM dei lettori sono qui:
   
   * [Browser TVSDK per HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con il token di licenza in mano, il client ora può derivare l&#39;URL della richiesta dal token, effettuare la richiesta di licenza per ExpressPlay, quindi riprodurre il contenuto selezionato per l&#39;utente.
