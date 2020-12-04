---
description: Quando i metadati DRM di un video sono inclusi nel flusso multimediale, eseguite l'autenticazione durante la riproduzione.
seo-description: Quando i metadati DRM di un video sono inclusi nel flusso multimediale, eseguite l'autenticazione durante la riproduzione.
seo-title: Autenticazione DRM durante la riproduzione
title: Autenticazione DRM durante la riproduzione
uuid: a1a63e3e-be34-49e1-96c4-ae266003b3d1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Autenticazione DRM durante la riproduzione {#drm-authentication-during-playback}

Quando i metadati DRM di un video sono inclusi nel flusso multimediale, eseguite l&#39;autenticazione durante la riproduzione.

Considerate la funzione di rotazione della licenza, in cui una risorsa viene crittografata con più licenze DRM. Ogni volta che vengono individuati nuovi metadati DRM, utilizzate i metodi `DRMHelper` per verificare se i metadati DRM richiedono l&#39;autenticazione DRM.

>[!NOTE]
>
>Questa esercitazione non gestisce le licenze con binding di dominio. Idealmente, prima di avviare la riproduzione, verificare se si tratta di una licenza con associazione a dominio. In caso affermativo, eseguite l&#39;autenticazione del dominio (se necessario) e iscrivetevi al dominio.

1. Quando in una risorsa vengono rilevati nuovi metadati DRM, viene inviato un evento a livello di applicazione.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. Utilizzate `DRMMetadata` per verificare se l&#39;autenticazione è necessaria. In caso contrario, non fare nulla; la riproduzione continua senza interruzioni.
1. In caso contrario, eseguite l&#39;autenticazione DRM. Poiché questa operazione è asincrona e viene gestita in un thread diverso, non ha alcun impatto sull&#39;interfaccia utente né sulla riproduzione video.
1. Se l’autenticazione non riesce, l’utente non può continuare a visualizzare il video e la riproduzione non riesce. In caso contrario, la riproduzione continuerà ininterrottamente.

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
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
