---
description: Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l'autenticazione prima di avviare la riproduzione.
seo-description: Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l'autenticazione prima di avviare la riproduzione.
seo-title: Autenticazione DRM prima della riproduzione
title: Autenticazione DRM prima della riproduzione
uuid: 6b4fbcfb-95fd-4591-bbb2-a17afd783383
translation-type: tm+mt
source-git-commit: 16b88f07468811f2c84decb1324b0c5bd2372131
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%

---


# Autenticazione DRM prima della riproduzione {#drm-authentication-before-playback}

Quando i metadati DRM di un video sono separati dal flusso multimediale, è necessario eseguire l&#39;autenticazione prima di avviare la riproduzione.

Una risorsa video può avere un file di metadati DRM associato, ad esempio:

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

In questo esempio, potete utilizzare i metodi `DRMHelper` per scaricare il contenuto del file di metadati DRM, analizzarlo e verificare se è necessaria l&#39;autenticazione DRM.

1. Utilizzate `loadDRMMetadata` per caricare il contenuto dell&#39;URL dei metadati e analizzare i byte scaricati in un `DRMMetadata`.

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

1. Informare l&#39;utente che questa operazione è asincrona, è consigliabile renderlo consapevole.

   Se gli utenti non sanno che l&#39;operazione è asincrona, potrebbero chiedersi perché la riproduzione non sia ancora iniziata. Ad esempio, potete visualizzare una ruota di selezione mentre i metadati DRM vengono scaricati e analizzati.

1. Implementa le callback in `DRMLoadMetadataListener`.

   La `loadDRMMetadata` richiama questi gestori eventi.

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

   * `onLoadMetadataUrlStart` rileva l’inizio del caricamento dell’URL dei metadati.
   * `onLoadMetadataUrlComplete` rileva il termine del caricamento dell’URL dei metadati.
   * `onLoadMetadataUrlError` indica che il caricamento dei metadati non è riuscito.

1. Al termine del caricamento, ispezionare l&#39;oggetto `DRMMetadata` per determinare se è necessaria l&#39;autenticazione DRM.

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

1. Completa una delle attività seguenti:

   * Se l&#39;autenticazione non è necessaria, avviate la riproduzione.
   * Se è richiesta l&#39;autenticazione, completare l&#39;autenticazione acquisendo la licenza.

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

1. Utilizzare un listener di eventi per controllare lo stato di autenticazione.

   Questo processo richiede la comunicazione in rete, quindi anche questa è un&#39;operazione asincrona.

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

1. Se l&#39;autenticazione ha esito positivo, avviate la riproduzione.
1. Se l&#39;autenticazione non ha esito positivo, avvisate l&#39;utente e non avviate la riproduzione.

   L&#39;applicazione deve gestire eventuali errori di autenticazione. Se l&#39;autenticazione non viene eseguita correttamente prima della riproduzione, TVSDK viene collocato in uno stato di errore e la riproduzione si arresta. L’applicazione deve risolvere il problema, ripristinare il lettore e ricaricare la risorsa.
