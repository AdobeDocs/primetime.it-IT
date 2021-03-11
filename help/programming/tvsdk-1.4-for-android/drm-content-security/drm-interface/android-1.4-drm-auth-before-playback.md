---
description: Quando i metadati DRM di un video sono separati dal flusso multimediale, eseguire l'autenticazione prima di iniziare la riproduzione.
title: Autenticazione DRM prima della riproduzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 1%

---


# Autenticazione DRM prima della riproduzione {#drm-authentication-before-playback}

Quando i metadati DRM di un video sono separati dal flusso multimediale, eseguire l&#39;autenticazione prima di iniziare la riproduzione.

A una risorsa video può essere associato un file di metadati DRM. Ad esempio:

* &quot;url&quot;: &quot;ht<span></span>tps://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;: &quot;ht<span></span>tps://www.domain.com/asset.metadata&quot;

In questo caso, utilizza i metodi `DRMHelper` per scaricare il contenuto del file di metadati DRM, analizzarlo e verificare se è necessaria l’autenticazione DRM.

1. Utilizza `loadDRMMetadata` per caricare il contenuto dell&#39;URL dei metadati e analizzare i byte scaricati in un `DRMMetadata`.

   Come qualsiasi altra operazione di rete, questo metodo è asincrono, creando il proprio thread.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Ad esempio:

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. Poiché l’operazione è asincrona, è consigliabile renderla consapevole. Altrimenti, si chiederà perché la sua riproduzione non è in fase di avvio. Ad esempio, mostra una ruota rotante mentre i metadati DRM vengono scaricati e analizzati.
1. Implementa i callback in `DRMLoadMetadataListener`. Il `loadDRMMetadata` chiama questi gestori eventi (invia questi eventi).

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

   * `onLoadMetadataUrlStart` rileva quando è iniziato il caricamento dell&#39;URL dei metadati.
   * `onLoadMetadataUrlComplete` rileva quando l&#39;URL dei metadati ha terminato il caricamento.
   * `onLoadMetadataUrlError` indica che non è stato possibile caricare i metadati.

1. Al termine del caricamento, controlla l’oggetto `DRMMetadata` per verificare se è necessaria l’autenticazione DRM.

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. Se l&#39;autenticazione non è necessaria, avviare la riproduzione.
1. Se è necessaria l’autenticazione, esegui l’autenticazione acquisendo la licenza.

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

   Questo esempio, per semplicità, codifica esplicitamente il nome e la password dell&#39;utente.

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   ```

1. Ciò implica anche la comunicazione in rete, quindi anche questa è un&#39;operazione asincrona. Utilizza un listener di eventi per controllare lo stato di autenticazione.

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   ```

1. Se l&#39;autenticazione ha esito positivo, avviare la riproduzione.
1. Se l&#39;autenticazione non ha esito positivo, avvisa l&#39;utente e non avvia la riproduzione.

L&#39;applicazione deve gestire eventuali errori di autenticazione. Impossibile eseguire l&#39;autenticazione prima che TVSDK venga riprodotto in uno stato di errore. In altre parole, cambia lo stato in ERROR, viene generato un errore contenente il codice di errore dalla libreria DRM e la riproduzione si arresta. L’applicazione deve risolvere il problema, reimpostare il lettore e ricaricare la risorsa.

