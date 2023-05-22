---
description: Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l’autenticazione prima di iniziare la riproduzione.
title: Autenticazione DRM prima della riproduzione
exl-id: b3267363-f734-44a6-99f5-e155deb53f3e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Autenticazione DRM prima della riproduzione {#drm-authentication-before-playback}

Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l’autenticazione prima di iniziare la riproduzione.

A una risorsa video può essere associato un file di metadati DRM, ad esempio:

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

In questo esempio, puoi utilizzare `DRMHelper` metodi per scaricare il contenuto del file di metadati DRM, analizzarlo e verificare se è necessaria l&#39;autenticazione DRM.

1. Utilizzare `loadDRMMetadata` per caricare il contenuto dell’URL dei metadati e analizzare i byte scaricati in una `DRMMetadata`.

   >[!TIP]
   >
   >Questo metodo è asincrono e crea un proprio thread.

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

1. Avvisa l&#39;utente che l&#39;operazione è asincrona. È consigliabile informare l&#39;utente.

   Se gli utenti non sanno che l’operazione è asincrona, potrebbero chiedersi perché la riproduzione non è ancora iniziata. È possibile, ad esempio, visualizzare una ruota di selezione durante il download e l&#39;analisi dei metadati DRM.

1. Implementare i callback in `DRMLoadMetadataListener`.

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

   * `onLoadMetadataUrlStart` rileva quando è iniziato il caricamento dell’URL dei metadati.
   * `onLoadMetadataUrlComplete` rileva quando l’URL dei metadati è stato caricato.
   * `onLoadMetadataUrlError` indica che il caricamento dei metadati non è riuscito.

1. Al termine del caricamento, controllare `DRMMetadata` per determinare se è necessaria l&#39;autenticazione DRM.

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

   * Se non è richiesta l’autenticazione, avvia la riproduzione.
   * Se è richiesta l’autenticazione, completa l’autenticazione acquisendo la licenza.

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

      In questo esempio, per semplicità, il nome e la password dell’utente sono codificati esplicitamente:

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

   Questo processo implica la comunicazione di rete, quindi anche questa è un&#39;operazione asincrona.

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

1. Se l’autenticazione ha esito positivo, avvia la riproduzione.
1. Se l’autenticazione non ha esito positivo, avvisa l’utente e non avvia la riproduzione.

   L&#39;applicazione deve gestire tutti gli errori di autenticazione. Impossibile eseguire l’autenticazione prima che la riproduzione presenti TVSDK in uno stato di errore, e la riproduzione si interrompe. L&#39;applicazione deve risolvere il problema, reimpostare il lettore e ricaricare la risorsa.
