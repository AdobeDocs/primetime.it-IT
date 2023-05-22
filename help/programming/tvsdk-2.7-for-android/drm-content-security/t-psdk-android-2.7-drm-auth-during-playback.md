---
description: Quando i metadati DRM di un video sono inclusi nel flusso multimediale, è possibile eseguire l'autenticazione durante la riproduzione.
title: autenticazione DRM durante la riproduzione
exl-id: f6e6e73a-d455-4b2c-b35c-2db173372092
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# autenticazione DRM durante la riproduzione {#drm-authentication-during-playback}

Quando i metadati DRM di un video sono inclusi nel flusso multimediale, è possibile eseguire l&#39;autenticazione durante la riproduzione.

Con la rotazione delle licenze, una risorsa viene crittografata con più licenze DRM. Ogni volta che vengono rilevati nuovi metadati DRM, il `DRMHelper` vengono utilizzati metodi per verificare se i metadati DRM richiedono l&#39;autenticazione DRM.

>[!TIP]
>
>Prima di iniziare la riproduzione, verifica se si sta utilizzando una licenza associata al dominio e se è richiesta l’autenticazione del dominio. In caso affermativo, completa l’autenticazione del dominio e aggiungi al dominio.

1. Quando vengono rilevati nuovi metadati DRM in una risorsa, viene inviato un evento a livello di applicazione.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. Utilizza il `DRMMetadata` per verificare se è necessaria l&#39;autenticazione.

   * Se non è richiesta l&#39;autenticazione, non è necessario eseguire alcuna operazione e la riproduzione continua senza interruzioni.
   * Se è richiesta l&#39;autenticazione, completare l&#39;autenticazione DRM.

      Poiché questa operazione è asincrona e viene gestita in un thread diverso, non ha alcun impatto sull’interfaccia utente o sulla riproduzione video.

1. Se l’autenticazione non riesce, l’utente non può continuare a visualizzare il video e la riproduzione si interrompe.

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

Ad esempio:

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
 
        }); 
    } 
}; 
```
