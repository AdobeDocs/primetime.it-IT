---
description: Per implementare FairPlay Streaming nella tua app TVSDK, devi scrivere un Resource Loader, che invia una richiesta di acquisizione della licenza al tuo server FairPlay Streaming.
seo-description: Per implementare FairPlay Streaming nella tua app TVSDK, devi scrivere un Resource Loader, che invia una richiesta di acquisizione della licenza al tuo server FairPlay Streaming.
seo-title: Apple FairPlay nelle applicazioni TVSDK
title: Apple FairPlay nelle applicazioni TVSDK
uuid: 4384d379-37cd-46c5-8c25-0cda16bdebb8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# Apple FairPlay nelle applicazioni TVSDK {#apple-fairplay-in-tvsdk-applications}

Per implementare FairPlay Streaming nella tua app TVSDK, devi scrivere un Resource Loader, che invia una richiesta di acquisizione della licenza al tuo server FairPlay Streaming.

Il codice Resource Loader è responsabile delle seguenti attività:

1. Stabilire dove inviare la richiesta di acquisizione della licenza.
1. Formattate la richiesta.
1. Fornire le informazioni necessarie al server, in modo che il server possa decidere se la richiesta deve essere consentita.

Ad esempio, se state utilizzando  Adobe  DRM di Primetime Cloud basato su ExpressPlay, Resource Loader invia la richiesta a:

```
https://fp-gen.service.expressplay.com
```

Resource Loader formatta la richiesta e allega un token ExpressPlay che autorizza la riproduzione all&#39;URL. Quando si acquisisce il token ExpressPlay, è possibile considerare diverse opzioni. Queste opzioni sono determinate dalla modalità di creazione del pacchetto del contenuto.

Quando create il pacchetto del contenuto, il packager inserisce gli URL `skd:` nel manifesto M3U8. Dopo la voce `skd:`, è possibile inserire qualsiasi dato nel manifesto. È possibile utilizzare questi dati nel codice dell&#39;applicazione per completare le attività elencate sopra. Ad esempio, potete utilizzare `skd:{content_id}` in modo che l&#39;app possa determinare l&#39;ID del contenuto in corso di riproduzione e richiedere un token per quel contenuto specifico. Potete anche utilizzare `skd:{entitlement_server_url}?cid={content_id}`, in modo che l&#39;app non debba avere l&#39;URL del server di adesione hardcoded.

Potrebbe non essere necessario inserire informazioni nell&#39;URL `skd:` se, all&#39;avvio della riproduzione, si conosce già l&#39;ID contenuto attraverso altri canali. Il secondo esempio è una soluzione ideale per testare la configurazione, ma è anche possibile utilizzarla in un ambiente di produzione.

>[!TIP]
>
>È possibile determinare il formato di `skd:`.

Il contenuto viene ottenuto utilizzando il protocollo `skd:`, ma la richiesta di licenza utilizza `https:`. Le opzioni più comuni per gestire questi protocolli sono:

* **Test iniziale della** riproduzione end-to-endQuando create il pacchetto del contenuto, selezionate un  `skd:` URL. Durante il test dell&#39;app, acquisite manualmente una licenza da ExpressPlay e codificate la licenza (un URL `https:`) e l&#39;URL del contenuto nel caricatore.

   Ad esempio:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **La maggior parte degli altri** casiQuando create il pacchetto del contenuto, selezionate un  `skd:` URL che rappresenti in modo univoco l’ID del contenuto. Nel caricatore, analizzate l&#39; `skd:` URL, inviatelo al server per acquisire un token e utilizzate il token risultante come URL.

   Ad esempio:

   ```
   - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
         shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
       NSURL *url = [[loadingRequest request] URL]; 
       if (![[url scheme] isEqual:@"skd"]) 
           return NO; 
   
       NSString *strUrl = [url absoluteString]; 
       NSLog(@"url is: %@", strUrl); 
   
       strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
   
       NSData *assetId; 
   
       NSData *requestBytes; 
       NSError* error = nil; 
       BOOL handled = NO; 
   
       NSData  *responseData = nil; 
   
       assetId = getMyAssetIdentifierFromURL(url); 
   
       /* Usecase 1: "On Premise Fairplay Server" 
        * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
        * Server Url is either hardcoded in the App or derived from strUrl. 
        */ 
   #if 0  
       // Insert your use case 1 codes here: 
       // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
   #endif // 
   
       /* Usecase 2: The strUrl is the entitlement server. 
        * Send assetId to the entitlement server; if the user is allowed to playback  
        * the content, the entitlement server will send back an ExpressPlay Token Url. 
        */ 
   
   #if 0 
       // The hardcoded SEES server: 
       strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
   
       // You can use the following code to simulate a device binding entitlement  
       // request:  
       // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
       // bEnforceDeviceID set to false. When you play the content, the device_id  
       // will be registered on the ExpressPlay Server.  Now change code to set  
       // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
       // sent back by the SEES server will be device bound. 
   
       // The strUrl returned below is the ExpressPlay Token URL. 
       strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
   #endif 
   
       /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
        */ 
   
       // Read in the certificate 
       NSLog(@"Get Application Certificate"); 
       NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                            ofType:nil]; 
   
       NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
   
       // To create the request blob for the server: 
       requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                         contentIdentifier:assetId  
                                                                   options:nil  
                                                                     error:&error]; 
       if (requestBytes == nil) { 
           NSLog(@"Error creating server request: %@", error); 
           return false; 
       } 
       // Per the specification, send requestBytes along with the assetId to the Key 
       // Server and obtain the response. 
       NSError *err; 
   
       responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
   
       if (responseData != nil) { 
           NSLog(@"Get response data: "); 
           [loadingRequest finishLoadingWithResponse:nil  
                                                data:(NSData *)responseData 
                                            redirect:nil]; 
       } 
       else { 
           [loadingRequest finishLoadingWithError:err]; 
           NSLog(@"bad key response"); 
       } 
       handled = YES; 
   bail: 
       return handled; 
   
   }
   ```

## Abilita Apple FairPlay nelle applicazioni TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.

1. Crea il caricatore di risorse cliente FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Per ulteriori informazioni, consultate [Apple FairPlay in applicazioni TVSDK](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Assicurati di seguire le istruzioni riportate nella *Guida al programma di streaming FairPlay* ( *FairPlayStreaming_PG.pdf*), inclusa in [FairPlay Server SDK per lo sviluppo di un&#39;app in base a FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Il metodo `resourceLoader:shouldWaitForLoadingOfRequestedResource` equivale a quello presente in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Nello scenario del server licenze ExpressPlay, per riprodurre contenuto, modificate lo schema URL nell&#39;URL della richiesta di licenza del server ExpressPlay FairPlay da `skd://` a `https://` (o `https://`).

1. Registrare il caricatore di risorse cliente *FairPlay* con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se avete scritto il vostro server licenze FairPlay o state utilizzando un server licenze FairPlay di terze parti, consultate il fornitore del server licenze per determinare l’URL del server licenze, la formattazione e altri requisiti.