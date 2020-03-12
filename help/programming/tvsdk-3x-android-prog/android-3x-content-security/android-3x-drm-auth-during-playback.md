---
description: Quando i metadati DRM di un video sono inclusi nel flusso multimediale, potete eseguire l'autenticazione durante la riproduzione.
seo-description: Quando i metadati DRM di un video sono inclusi nel flusso multimediale, potete eseguire l'autenticazione durante la riproduzione.
seo-title: Autenticazione DRM durante la riproduzione
title: Autenticazione DRM durante la riproduzione
uuid: d44acfb2-796b-4c60-b622-db01e58042cc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Autenticazione DRM durante la riproduzione {#drm-authentication-during-playback}

Quando i metadati DRM di un video sono inclusi nel flusso multimediale, potete eseguire l&#39;autenticazione durante la riproduzione.

Con la rotazione della licenza, una risorsa viene crittografata con più licenze DRM. Ogni volta che vengono scoperti nuovi metadati DRM, i `DRMHelper` metodi vengono utilizzati per verificare se i metadati DRM richiedono l&#39;autenticazione DRM.

>[!TIP]
>
>Prima di avviare la riproduzione, determinare se si tratta di una licenza associata a un dominio e se è necessaria l&#39;autenticazione del dominio. Se sì, completa l’autenticazione del dominio e partecipa al dominio.

1. Quando in una risorsa vengono rilevati nuovi metadati DRM, viene inviato un evento a livello di applicazione.

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

1. Utilizzate l&#39;icona `DRMMetadata` per verificare se è necessaria l&#39;autenticazione.

   * Se l’autenticazione non è necessaria, non è necessario eseguire alcuna operazione e la riproduzione continua senza interruzioni.
   * Se è richiesta l&#39;autenticazione, completa l&#39;autenticazione DRM.

      Poiché questa operazione è asincrona e viene gestita in un thread diverso, non ha alcun impatto sull&#39;interfaccia utente né sulla riproduzione video.

1. Se l’autenticazione non riesce, l’utente non può continuare a visualizzare il video e la riproduzione si arresta.

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
