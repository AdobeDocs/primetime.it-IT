---
description: È possibile utilizzare Adobe Offline packager per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.
title: Pacchetto Primetime / Cloud DRM / TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Pacchetto Primetime / Cloud DRM / TVSDK {#primetime-packager-cloud-drm-tvsdk}

È possibile utilizzare Adobe Offline packager per preparare i contenuti per qualsiasi soluzione DRM supportata da Primetime Cloud DRM, basata su ExpressPlay.

Questa serie di istruzioni presuppone che tu abbia già configurato un account amministratore ExpressPlay: [Avvio rapido di Primetime DRM Cloud](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. Scegliere l&#39;infrastruttura da utilizzare per la creazione di pacchetti dei contenuti. Primetime Packager supporta sia il packaging basato su riga di comando che sulla configurazione dei contenuti da utilizzare con le DRM FairPlay, Widevine e PlayReady. I seguenti formati e crittografia sono attualmente supportati in TVSDK (con ulteriori informazioni nella pipeline):

   * DASH (CENC) / PlayReady, Widevine - Per HTML5
   * HLS / FairPlay, Accesso - Per iOS

1. Scegli un sistema di gestione delle chiavi (KMS):

   * Utilizzare i KMS di ExpressPlay ( [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/)); questo sistema gestisce le chiavi di contenuto tramite l&#39;API RESTful di ExpressPlay.

      o...

   * Imposta il tuo KMS. Crea un database di chiavi di contenuto, selezionabile da Content-ID.

      In entrambi i casi, il KMS gestisce una fornitura di chiavi di contenuto, con ogni chiave con un Content-ID associato.

1. Crea un pacchetto per il contenuto. Con Primetime Packager è possibile creare pacchetti di contenuti per una soluzione DRM specifica o per più soluzioni DRM.

   I seguenti comandi di esempio mostrano alcuni esempi di creazione di pacchetti di contenuti per diverse soluzioni DRM:

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

   * [FairPlay con Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20)  (genera un file M3U8):

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
      >Il valore `key_url` viene copiato così come si trova nel file M3U8.

1. Crea un &quot;server di vetrina&quot;.

       Il server di vetrina deve gestire le seguenti operazioni:
   
   1. Selezione del contenuto da parte del cliente. Questa implementazione deve includere un endpoint per i client per richiedere un token di contenuto per un ID di contenuto specifico.
   1. Adesione del cliente
   1. Richieste di token di licenza (ExpressPlay) dal client ( [richiesta di token di licenza ExpressPlay / riferimento di risposta](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. Crea il tuo client.

       Il client deve includere una chiamata al server di vetrina. L’Adobe consiglia al client di chiamare la vetrina dopo che l’utente ha selezionato del contenuto e dopo che l’utente è autenticato. Quindi, passa il token restituito da ExpressPlay al tuo lettore per utilizzare per le richieste di licenza. Le presentazioni per l&#39;implementazione del componente DRM dei tuoi giocatori sono qui:
   
   * [Browser TVSDK per HTML5](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Con il token di licenza in mano, il client ora può derivare l’URL della richiesta dal token ed effettuare la richiesta di licenza a ExpressPlay, quindi riprodurre il contenuto selezionato per l’utente.
