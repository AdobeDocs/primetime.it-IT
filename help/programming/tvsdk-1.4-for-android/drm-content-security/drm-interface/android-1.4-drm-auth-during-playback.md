---
description: Quando i metadati DRM di un video sono inclusi nel flusso multimediale, eseguire l'autenticazione durante la riproduzione.
title: autenticazione DRM durante la riproduzione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# autenticazione DRM durante la riproduzione {#drm-authentication-during-playback}

Quando i metadati DRM di un video sono inclusi nel flusso multimediale, eseguire l&#39;autenticazione durante la riproduzione.

Consideriamo la funzione di rotazione delle licenze, in cui una risorsa è crittografata con più licenze DRM. Ogni volta che vengono rilevati nuovi metadati DRM, utilizzare `DRMHelper` metodi per verificare se i metadati DRM richiedono l&#39;autenticazione DRM.

>[!NOTE]
>
>Questa esercitazione non gestisce le licenze associate al dominio. Idealmente, prima di iniziare la riproduzione, verifica se si sta trattando con una licenza legata al dominio. In caso affermativo, esegui l’autenticazione del dominio (se necessario) e aggiungi al dominio.

1. Quando vengono rilevati nuovi metadati DRM in una risorsa, viene inviato un evento a livello di applicazione.

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

1. Utilizza il `DRMMetadata` per verificare se è necessaria l&#39;autenticazione. In caso contrario, non viene eseguita alcuna operazione; la riproduzione continua senza interruzioni.
1. In caso contrario, eseguire l&#39;autenticazione DRM. Poiché questa operazione è asincrona e viene gestita in un thread diverso, non ha alcun impatto sull’interfaccia utente o sulla riproduzione video.
1. Se l’autenticazione non riesce, l’utente non può continuare a visualizzare il video e la riproduzione cessa. In caso contrario, la riproduzione continuerà senza interruzioni.

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
