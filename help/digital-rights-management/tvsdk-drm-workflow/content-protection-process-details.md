---
title: Dettagli del processo di acquisizione delle licenze
description: Dettagli del processo di acquisizione delle licenze
copied-description: true
exl-id: d772339a-8d05-401b-b5c1-18169b3627b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Dettagli del processo di acquisizione delle licenze {#license-acquisition-process-details}

Questo processo presenta una vista dettagliata a livello di API del flusso di lavoro con contenuti protetti da DRM di Primetime:

1. Utilizzo di un `URLLoader` , caricare i byte del file di metadati del contenuto protetto.

   Imposta questo oggetto su una variabile, ad esempio `metadata_bytes`. Tutti i contenuti controllati da Primetime DRM dispongono di metadati DRM di Primetime. Quando il contenuto viene inserito in un pacchetto, i metadati possono essere salvati come file di metadati separato ( [!DNL .metadata]) insieme al contenuto. In alternativa, i metadati possono essere codificati in Base64 e inseriti nel corpo del file manifesto video. Per ulteriori informazioni, consulta [Creazione pacchetti di file multimediali](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Se necessario, rimuovere il punto esclamativo `!` dall&#39;inizio della stringa.
   1. Se necessario per il contenuto HLS o HDS, decodificare i metadati inclusi nella stringa con codifica Base64 in dati binari prima di trasmetterli.
1. Creare un `DRMContentData` dell&#39;istanza.

   Inserisci questo codice in un blocco try-catch:

   ```
   new DRMContentData(metadata_bytes)
   ```

   dove `metadata_bytes` è il `URLLoader` oggetto ottenuto nel passaggio 1.

   [iOS: metadati DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Creare listener per l&#39;ascolto `DRMStatusEvent` e `DRMErrorEvent` inviato da `DRMManager` oggetto.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   In `DRMStatusEvent` listener, verificare che la licenza sia valida (non null). In `DRMErrorEvent` listener, handle `DRMErrorEvents`. Consulta *Utilizzo della classe DRMStatusEvent* e *Utilizzo della classe DRMErrorEvent* in questa guida.

1. Carica la licenza necessaria per riprodurre il contenuto.
Innanzitutto, prova a caricare una licenza memorizzata localmente per riprodurre il contenuto:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   Al termine del caricamento, il `DRMManager` invii di oggetti `DRMStatusEvent.DRM_Status`.

1. Controlla la `DRMVoucher` oggetto.


   Se il `DRMVoucher` l&#39;oggetto non è nullo, la licenza è valida. Passare al punto 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Controlla il metodo di autenticazione richiesto dal criterio per questo contenuto.

   Utilizza il `DRMContentData.authenticationMethod` proprietà.
   1. Se il metodo di autenticazione è `ANONYMOUS`, andare al passaggio 9. 

      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Se il metodo di autenticazione è `USERNAME_AND_PASSWORD`, l’applicazione deve fornire un meccanismo che consenta all’utente di immettere le credenziali.

      Passa le credenziali dell&#39;utente al server licenze per autenticare l&#39;utente:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      Il `DRMManager` invia un `DRMAuthenticationErrorEvent` se l’autenticazione non riesce, oppure `DRMAuthenticationCompleteEvent` se l’autenticazione ha esito positivo. Creare listener per questi eventi.

      [Android: authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autentica:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >L’Adobe consiglia di utilizzare un meccanismo più sicuro per fornire le credenziali. Per maggiori informazioni, vedere [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Se il metodo di autenticazione è `UNKNOWN`, è necessario utilizzare un metodo di autenticazione personalizzato.

      In questo caso, il provider di contenuti ha disposto che l’autenticazione venga eseguita in modo fuori banda, non utilizzando le API Primetime. La procedura di autenticazione personalizzata deve produrre un token di autenticazione che può essere passato al `DRMManager.setAuthenticationToken()` metodo.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >In alternativa, indipendentemente dal metodo di autenticazione, `.setAuthenticationToken()` può essere utilizzato per inviare dati personalizzati dal client al server licenze. Si tratta di un sovraccarico dell’API, in quanto questo meccanismo è l’unico modo per inviare dati dinamici personalizzati dal client al server licenze al momento dell’acquisizione della licenza. Questo metodo di trasporto dei dati personalizzati viene discusso in modo approfondito in diversi post del forum in [Forum DRM (Adobe Access) di Primetime ](https://forums.adobe.com/community/adobe_access).

1. Se l&#39;autenticazione non riesce, l&#39;applicazione deve tornare al passaggio 6.

   Assicurati che l’applicazione disponga di un meccanismo per gestire e limitare gli errori di autenticazione ripetuti. Ad esempio, dopo tre tentativi, viene visualizzato un messaggio per indicare che l’autenticazione non è riuscita e che non è possibile riprodurre il contenuto.
1. Per utilizzare il token memorizzato invece di richiedere all’utente di immettere le credenziali, imposta il token con `DRMManager.setAuthenticationToken()` metodo.

   Quindi scaricate la licenza dal server licenze e riproducete il contenuto come indicato al punto 6.
   1. **Facoltativo:** Se l&#39;autenticazione ha esito positivo, puoi acquisire il token di autenticazione, che è una matrice di byte memorizzata nella cache.

      Ottieni questo token con `DRMAuthenticationCompleteEvent.token` proprietà. Puoi archiviare e utilizzare il token di autenticazione in modo che l’utente non debba immettere ripetutamente le credenziali per questo contenuto. Il server licenze determina il periodo valido del token di autenticazione.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Se l&#39;autenticazione ha esito positivo, scaricare la licenza dal server licenze:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   Al termine del caricamento, il `DRMManager` invii di oggetti `DRMStatusEvent.DRM_STATUS`. Ascolta questo evento e, una volta inviato, puoi riprodurne il contenuto.  Riproduci il video creando un oggetto Primetime e chiamando il relativo `play()` metodo:

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android: acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)
