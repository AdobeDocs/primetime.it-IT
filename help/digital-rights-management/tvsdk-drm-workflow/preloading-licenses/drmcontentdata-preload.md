---
title: Utilizzo di DRMContentData per precaricare le licenze
description: Utilizzo di DRMContentData per precaricare le licenze
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Utilizzo di DRMContentData per precaricare le licenze{#using-drmcontentdata-to-pre-load-licenses}

I passaggi seguenti descrivono il flusso di lavoro per precaricare la licenza per un file multimediale protetto utilizzando un `DRMContentData` oggetto.

1. Ottenere i metadati DRM binari per il contenuto del pacchetto.

   Se si utilizza Primetime DRM Java Reference Implementations Packager, questo file di metadati viene generato automaticamente con un [!DNL .metadata] estensione. Ad esempio, puoi scaricare questi metadati utilizzando `URLLoader` classe. Se si utilizza contenuto HLS o HDS, nel file del manifesto del contenuto viene fatto riferimento ai metadati ( [!DNL .m3u8] o [!DNL .f4m]) o incluso *entro* il file manifesto come stringa con codifica Base64 (che deve essere decodificata Base64 prima del consumo).
1. Creare un `DRMContentData` , passando i metadati alla funzione di costruzione:

   ```
   var drmData:DRMContentData = new DRMContentData( metadata );
   ```

1. Gli altri passaggi sono identici al flusso di lavoro descritto in *Dettagli del processo di protezione dei contenuti*.

<!--<a id="example_EBEDA8E10F6344CABA4DE31DC342B8F8"></a>-->

```
import flash.events.DRMAuthenticationCompleteEvent; 
import flash.events.DRMAuthenticationErrorEvent; 
import flash.events.DRMErrorEvent; 
import flash.events.DRMStatusEvent; 
import flash.events.NetStatusEvent; 
import flash.net.NetConnection; 
import flash.net.Primetime; 
import flash.net.PrimetimePlayOptions; 
import flash.net.drm.AuthenticationMethod; 
import flash.net.drm.DRMContentData; 
import flash.net.drm.DRMManager; 
import flash.net.drm.LoadVoucherSetting; 
  
public class DRMPreloader extends Sprite  { 
    private var videoURL:String = "app-storage:/video.flv"; 
    private var userName:String = "user"; 
    private var password:String = "password"; 
    private var preloadConnection:NetConnection; 
    private var preloadStream:Primetime; 
    private var drmManager:DRMManager = DRMManager.getDRMManager(); 
 
    private var drmContentData:DRMContentData; 
 
    public function DRMPreloader():void { 
        drmManager.addEventListener(  
          DRMAuthenticationCompleteEvent.AUTHENTICATION_COMPLETE,  
          onAuthenticationComplete 
        ); 
        drmManager.addEventListener( 
          DRMAuthenticationErrorEvent.AUTHENTICATION_ERROR,  
          onAuthenticationError 
        ); 
        drmManager.addEventListener( 
          DRMStatusEvent.DRM_STATUS, onDRMStatus); 
        drmManager.addEventListener( 
          DRMErrorEvent.DRM_ERROR, onDRMError); 
        preloadConnection = new NetConnection(); 
        preloadConnection.addEventListener( 
          NetStatusEvent.NET_STATUS, onConnect); 
        preloadConnection.connect(null);  
    } 
 
    private function onConnect( event:NetStatusEvent ):void {  
        preloadMetadata(); 
    } 
 
    private function preloadMetadata():void {  
        preloadStream = new Primetime( preloadConnection ); 
        preloadStream.client = this; 
        var options:PrimetimePlayOptions = new PrimetimePlayOptions(); 
        options.streamName = videoURL; 
        preloadStream.preloadEmbeddedData( options );  
    }  
 
    public function onDRMContentData( drmMetadata:DRMContentData ):void {  
        drmContentData = drmMetadata; 
        if ( drmMetadata.authenticationMethod ==  
               AuthenticationMethod.USERNAME_AND_PASSWORD ) {  
            authenticateUser(); 
        } 
        else {  
            getVoucher(); 
        } 
    } 
 
    private function getVoucher():void {  
        drmManager.loadVoucher(  
          drmContentData,  
          LoadVoucherSetting.ALLOW_SERVER  
        ); 
    } 
 
    private function authenticateUser():void {  
        drmManager.authenticate(  
          drmContentData.serverURL,  
          drmContentData.domain,  
          userName,  
          password  
        ); 
    } 
 
    private function onAuthenticationError(  
      event:DRMAuthenticationErrorEvent ):void {  
        trace( "Authentication error: " +  
               event.errorID + ", " +  
               event.subErrorID ); 
    } 
 
    private function onAuthenticationComplete(  
      event:DRMAuthenticationCompleteEvent ):void {  
        trace( "Authenticated to: " +  
               event.serverURL + ",  
               domain: " +  
               event.domain ); 
        getVoucher(); 
    } 
 
    private function onDRMStatus( event:DRMStatusEvent ):void { 
        trace( "DRM Status: " + event.detail); 
        trace("--License allows offline playback = " +  
              event.isAvailableOffline ); 
        trace("--License already cached = " +  
              event.isLocal ); 
        trace("--License required authentication = " +  
              !event.isAnonymous ); 
    } 
 
    private function onDRMError( event:DRMErrorEvent ):void { 
        trace( "DRM error event: " +  
               event.errorID + ", " +  
               event.subErrorID + ", " +  
               event.text ); 
    } 
 
    public function onPlayStatus( info:Object ):void { 
        preloadStream.close(); 
    }  
} 
```

