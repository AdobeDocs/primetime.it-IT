---
description: Quando i metadati DRM di un video sono separati dal flusso multimediale, eseguire l'autenticazione prima di iniziare la riproduzione.
title: Autenticazione DRM prima della riproduzione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Autenticazione DRM prima della riproduzione {#drm-authentication-before-playback}

Quando i metadati DRM di un video sono separati dal flusso multimediale, eseguire l&#39;autenticazione prima di iniziare la riproduzione.

A una risorsa video può essere associato un file di metadati DRM. Ad esempio:

* &quot;url&quot;: &quot;ht<span></span>tps://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;: &quot;ht<span></span>tps://www.domain.com/asset.metadata&quot;

In questo caso, utilizza `DRMHelper` metodi per scaricare il contenuto del file di metadati DRM, analizzarlo e verificare se è necessaria l&#39;autenticazione DRM.

1. Utilizzare `loadDRMMetadata` per caricare il contenuto dell’URL dei metadati e analizzare i byte scaricati in una `DRMMetadata`.

   Come qualsiasi altra operazione di rete, questo metodo è asincrono e crea il proprio thread.

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

1. Poiché l’operazione è asincrona, è consigliabile informare l’utente al riguardo. Altrimenti, si chiederà perché la sua riproduzione non inizia. Ad esempio, visualizzare una ruota di selezione durante il download e l&#39;analisi dei metadati DRM.
1. Implementare i callback in `DRMLoadMetadataListener`. Il `loadDRMMetadata` chiama questi gestori eventi (invia questi eventi).

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

   * `onLoadMetadataUrlStart` rileva quando è iniziato il caricamento dell’URL dei metadati.
   * `onLoadMetadataUrlComplete` rileva quando l’URL dei metadati è stato caricato.
   * `onLoadMetadataUrlError` indica che il caricamento dei metadati non è riuscito.

1. Al termine del caricamento, controllare `DRMMetadata` per verificare se è necessaria l&#39;autenticazione DRM.

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

1. Se l’autenticazione non è necessaria, avvia la riproduzione.
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

   Questo esempio, per semplicità, codifica esplicitamente il nome e la password dell’utente.

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

1. Questo implica anche la comunicazione di rete, quindi anche questa è un&#39;operazione asincrona. Utilizza un listener di eventi per controllare lo stato di autenticazione.

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

1. Se l’autenticazione ha esito positivo, avvia la riproduzione.
1. Se l’autenticazione non ha esito positivo, avvisa l’utente e non avvia la riproduzione.

L&#39;applicazione deve gestire tutti gli errori di autenticazione. Impossibile autenticare correttamente prima che TVSDK venga riprodotto in uno stato di errore. In altre parole, modifica il suo stato in ERRORE, viene generato un errore contenente il codice di errore della libreria DRM e la riproduzione si interrompe. L&#39;applicazione deve risolvere il problema, reimpostare il lettore e ricaricare la risorsa.
