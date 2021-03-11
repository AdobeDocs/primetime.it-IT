---
description: Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l'autenticazione prima di iniziare la riproduzione.
title: Autenticazione DRM prima della riproduzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---


# Autenticazione DRM prima della riproduzione {#drm-authentication-before-playback}

Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l&#39;autenticazione prima di iniziare la riproduzione.

Una risorsa video può avere un file di metadati DRM associato, ad esempio:

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

In questo esempio, puoi utilizzare i metodi `DRMHelper` per scaricare il contenuto del file di metadati DRM, analizzarlo e verificare se è necessaria l’autenticazione DRM.

1. Utilizza `loadDRMMetadata` per caricare il contenuto dell&#39;URL dei metadati e analizzare i byte scaricati in un `DRMMetadata`.

   >[!TIP]
   >
   >Questo metodo è asincrono e crea il proprio thread.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Ad esempio:

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. Notifica all&#39;utente che l&#39;operazione è asincrona; è consigliabile informare l&#39;utente in merito.

   Se gli utenti non sanno che l’operazione è asincrona, potrebbero chiedersi perché la riproduzione non è ancora iniziata. Ad esempio, puoi mostrare una ruota rotante mentre i metadati DRM vengono scaricati e analizzati.

1. Implementa i callback in `DRMLoadMetadataListener`.

   Il `loadDRMMetadata` chiama questi gestori eventi.

   ```java
   public interface DRMLoadMetadataListener { 
   
       public void onLoadMetadataUrlStart(); 
   
       /** 
       * @param authNeeded 
       * whether DRM authentication is needed. 
       * @param drmMetadata 
       * the parsed DRMMetadata obtained.    */ 
       public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata); 
       public void onLoadMetadataUrlError(); 
   } 
   ```

   Di seguito sono riportati ulteriori dettagli sui gestori:

   * `onLoadMetadataUrlStart` rileva quando è iniziato il caricamento dell&#39;URL dei metadati.
   * `onLoadMetadataUrlComplete` rileva quando l&#39;URL dei metadati ha terminato il caricamento.
   * `onLoadMetadataUrlError` indica che non è stato possibile caricare i metadati.

1. Al termine del caricamento, controlla l&#39;oggetto `DRMMetadata` per determinare se è necessaria l&#39;autenticazione DRM.

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   Ad esempio:

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. Completa una delle seguenti attività:

   * Se l&#39;autenticazione non è necessaria, avviare la riproduzione.
   * Se è necessaria l’autenticazione, completa l’autenticazione acquisendo la licenza.

      ```java
      /** 
      * Helper method to perform DRM authentication. 
      * 
      * @param drmManager 
      * the DRMManager, used to perform the authentication. 
      * @param drmMetadata 
      * the DRMMetadata, containing the DRM specific information. 
      * @param authenticationListener 
      * the listener, on which the user can be notified about the 
      * authentication process status. 
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      In questo esempio, per semplicità, il nome e la password dell&#39;utente sono codificati in modo esplicito:

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. Utilizza un listener di eventi per controllare lo stato di autenticazione.

   Questo processo implica la comunicazione in rete, quindi anche questa è un&#39;operazione asincrona.

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. Se l&#39;autenticazione ha esito positivo, avviare la riproduzione.
1. Se l&#39;autenticazione non ha esito positivo, avvisa l&#39;utente e non avvia la riproduzione.

   L&#39;applicazione deve gestire eventuali errori di autenticazione. Impossibile eseguire l&#39;autenticazione prima che la riproduzione riporti TVSDK in uno stato di errore e la riproduzione si interrompe. L’applicazione deve risolvere il problema, reimpostare il lettore e ricaricare la risorsa.
