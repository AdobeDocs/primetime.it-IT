---
seo-title: Dettagli del processo di acquisizione della licenza
title: Dettagli del processo di acquisizione della licenza
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Dettagli del processo di acquisizione della licenza {#license-acquisition-process-details}

Questo processo presenta una visualizzazione dettagliata a livello di API del flusso di lavoro del contenuto protetto DRM di Primetime:

1. Utilizzando un oggetto `URLLoader`, caricare i byte del file di metadati del contenuto protetto.

   Impostate questo oggetto su una variabile, ad esempio `metadata_bytes`. Tutti i contenuti controllati da DRM di Primetime hanno metadati DRM di Primetime. Quando viene creato un pacchetto, questi metadati possono essere salvati insieme al contenuto come un file di metadati separato ( [!DNL .metadata]). In alternativa, i metadati possono essere codificati con Base64 e inseriti nel corpo del file manifesto video. Per ulteriori informazioni, vedere [Creazione di pacchetti di file multimediali](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Se necessario, rimuovere il punto esclamativo `!` dall&#39;inizio della stringa.
   1. Se necessario per il contenuto HLS o HDS, decodificate i metadati inclusi nella stringa con codifica Base64 in dati binari prima di trasmetterli.
1. Create un&#39;istanza `DRMContentData`.

   Inserire questo codice in un blocco try-catch:

   ```
   new DRMContentData(metadata_bytes)
   ```

   dove `metadata_bytes` è l&#39;oggetto `URLLoader` ottenuto al punto 1.

   [iOS: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Creare listener per ascoltare l&#39;oggetto `DRMStatusEvent` e `DRMErrorEvent` inviato dall&#39;oggetto `DRMManager`.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   Nel listener `DRMStatusEvent` verificare che la licenza sia valida (non null). Nel listener `DRMErrorEvent`, gestire `DRMErrorEvents`. Vedere *Utilizzo della classe DRMStatusEvent* e *Utilizzo della classe DRMErrorEvent* in questa guida.

1. Caricate la licenza necessaria per riprodurre il contenuto.
Innanzitutto, caricate una licenza memorizzata localmente per riprodurre il contenuto:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.acquisitionLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: acquisitionLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   Al termine del caricamento, l&#39;oggetto `DRMManager` invia `DRMStatusEvent.DRM_Status`.

1. Controllare l&#39;oggetto `DRMVoucher`.


   Se l&#39;oggetto `DRMVoucher` non è nullo, la licenza è valida. Passate al punto 9.

   [Android: DRMLicenseAcquisredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseAcquisred](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Verificare il metodo di autenticazione richiesto dal criterio per il contenuto.

   Utilizzare la proprietà `DRMContentData.authenticationMethod`.
   1. Se il metodo di autenticazione è `ANONYMOUS`, passare al punto 9. 

      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Se il metodo di autenticazione è `USERNAME_AND_PASSWORD`, l&#39;applicazione deve fornire un meccanismo per consentire all&#39;utente di immettere le credenziali.

      Trasmettere le credenziali dell&#39;utente al server delle licenze per autenticare l&#39;utente:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      Il `DRMManager` invia un `DRMAuthenticationErrorEvent` se l&#39;autenticazione ha esito negativo oppure un `DRMAuthenticationCompleteEvent` se l&#39;autenticazione ha esito positivo. Creare listener per questi eventi.

      [Android: authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autenticare:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      > Adobe consiglia di utilizzare un meccanismo più sicuro per fornire le credenziali. Per ulteriori informazioni, vedere [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Se il metodo di autenticazione è `UNKNOWN`, è necessario utilizzare un metodo di autenticazione personalizzato.

      In questo caso, il fornitore di contenuti ha organizzato l&#39;autenticazione in modo fuori banda, non utilizzando le API Primetime. La procedura di autenticazione personalizzata deve produrre un token di autenticazione che può essere passato al metodo `DRMManager.setAuthenticationToken()`.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >In alternativa, indipendentemente dal metodo di autenticazione, è possibile utilizzare `.setAuthenticationToken()` per inviare dati personalizzati dal client al server licenze. Si tratta di un sovraccarico dell&#39;API, in quanto questo meccanismo è l&#39;unico modo per inviare dati personalizzati dinamici dal client al server licenze al momento dell&#39;acquisizione della licenza. Questo metodo di trasporto dei dati personalizzato viene discusso in modo approfondito in diversi post del forum nei forum [Primetime DRM ( Accesso Adobe) ](https://forums.adobe.com/community/adobe_access).

1. Se l&#39;autenticazione non riesce, l&#39;applicazione deve tornare al punto 6.

   Verificare che l&#39;applicazione disponga di un meccanismo per gestire e limitare i ripetuti errori di autenticazione. Ad esempio, dopo tre tentativi, viene visualizzato un messaggio all&#39;utente che indica che l&#39;autenticazione non è riuscita e che il contenuto non può essere riprodotto.
1. Per utilizzare il token memorizzato invece di richiedere all&#39;utente di immettere le credenziali, impostare il token con il metodo `DRMManager.setAuthenticationToken()`.

   Potete quindi scaricare la licenza dal server licenze e riprodurre il contenuto come nel passaggio 6.
   1. **Facoltativo:** Se l&#39;autenticazione ha esito positivo, è possibile acquisire il token di autenticazione, ovvero un array di byte memorizzato nella cache.

      Ottenete questo token con la proprietà `DRMAuthenticationCompleteEvent.token`. È possibile memorizzare e utilizzare il token di autenticazione in modo che l&#39;utente non debba immettere ripetutamente le credenziali per questo contenuto. Il server licenze determina il periodo valido del token di autenticazione.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Se l&#39;autenticazione ha esito positivo, scaricate la licenza dal server licenze:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   Al termine del caricamento, l&#39;oggetto `DRMManager` invia `DRMStatusEvent.DRM_STATUS`. Ascoltare questo evento e, quando viene inviato, riprodurre il contenuto.  Per riprodurre il video, create un oggetto Primetime e chiamatene il metodo `play()`:

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