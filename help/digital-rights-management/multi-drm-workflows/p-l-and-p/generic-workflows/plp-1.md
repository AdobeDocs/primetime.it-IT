---
description: È possibile utilizzare Offline Packager di Adobe per preparare i contenuti per le soluzioni DRM supportate da Primetime Cloud DRM, con tecnologia ExpressPlay.
title: Primetime Packager/Cloud DRM/TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Primetime Packager/Cloud DRM/TVSDK {#primetime-packager-cloud-drm-tvsdk}

È possibile utilizzare Offline Packager di Adobe per preparare i contenuti per le soluzioni DRM supportate da Primetime Cloud DRM, con tecnologia ExpressPlay.

Questa serie di istruzioni presuppone che sia già stato configurato un account amministratore ExpressPlay: [Avvio rapido di Primetime DRM Cloud](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Scegli l’infrastruttura da utilizzare per la creazione del pacchetto dei contenuti. Primetime Packager supporta sia la creazione di pacchetti di contenuti basati su riga di comando che su configurazione per l&#39;utilizzo con le DRM FairPlay, Widevine e PlayReady. I seguenti formati e crittografia sono attualmente supportati in TVSDK (con altri nella pipeline):

   * DASH (CENC) / PlayReady, Widevine - Per HTML5
   * HLS/FairPlay, accesso - Per iOS

1. Scegliere un sistema di gestione delle chiavi (KMS):

   * Utilizzare il KMS di ExpressPlay ( [Archiviazione chiavi ExpressPlay](https://www.expressplay.com/developer/key-storage/)); questo sistema gestisce le chiavi di contenuto tramite l&#39;API RESTful di ExpressPlay.

      o...

   * Configura il tuo KMS. Crea un database di chiavi di contenuto, selezionabili tramite Content-ID.

      In entrambi i casi, KMS gestisce una fornitura di chiavi di contenuto, a ciascuna delle quali è associato un Content-ID.

1. Creare un pacchetto dei contenuti. Con Primetime Packager è possibile creare un pacchetto di contenuti per una soluzione DRM specifica o per più soluzioni DRM.

   I comandi di esempio riportati di seguito mostrano alcuni esempi di creazione di pacchetti di contenuti per diverse soluzioni DRM:

   * [Widevine con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) (genera il file MPD):

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

   * [FairPlay con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) (Genera un file M3U8):

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
      >Il `key_url` viene copiato così come è nel file M3U8.

1. Creare un &quot;server storefront&quot;.

       Il server storefront deve gestire le seguenti operazioni:
   
   1. Selezione di contenuti da parte del cliente. Questa implementazione deve includere un endpoint per consentire ai client di richiedere un token di contenuto per un ID di contenuto specifico.
   1. Adesione cliente
   1. Richieste di token di licenza (ExpressPlay) dal client ( [Richiesta token di licenza ExpressPlay/riferimento di risposta](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Crea il client.

       Il client deve includere una chiamata al server storefront. L’Adobe consiglia al client di chiamare la vetrina dopo che l’utente ha selezionato alcuni contenuti e dopo che è stato autenticato. Quindi, passa il token restituito da ExpressPlay al lettore per utilizzarlo per le richieste di licenza. Le presentazioni per l’implementazione del componente DRM dei lettori sono disponibili qui:
   
   * [Browser TVSDK per HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con il token di licenza disponibile, il client può ora derivare l’URL della richiesta dal token, effettuare la richiesta di licenza a ExpressPlay e quindi riprodurre il contenuto selezionato per l’utente.
