---
description: Per implementare FairPlay Streaming nell’app TVSDK, devi scrivere un Caricatore di risorse che invia una richiesta di acquisizione della licenza al server FairPlay Streaming.
title: Apple FairPlay nelle applicazioni TVSDK
exl-id: 83fdc75b-f736-4091-ab80-e7f6e9723482
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Apple FairPlay nelle applicazioni TVSDK  {#apple-fairplay-in-tvsdk-applications}

Per implementare FairPlay Streaming nell’app TVSDK, devi scrivere un Caricatore di risorse che invia una richiesta di acquisizione della licenza al server FairPlay Streaming.

Il codice di Caricatore risorse è responsabile delle seguenti attività:

1. Determina dove inviare la richiesta di acquisizione della licenza.
1. Formatta la richiesta.
1. Fornisci le informazioni necessarie al server, in modo che possa decidere se la richiesta deve essere consentita.

Se ad esempio utilizzi Primetime Cloud DRM di Adobe basato su ExpressPlay, il caricatore di risorse invia la richiesta a:

```
https://fp-gen.service.expressplay.com
```

Il caricatore di risorse formatta la richiesta e allega un token ExpressPlay che autorizza la riproduzione nell’URL. Quando si acquista il token ExpressPlay, sono disponibili diverse opzioni da considerare. Queste opzioni sono determinate dalla modalità di creazione del pacchetto del contenuto.

Quando si crea il pacchetto del contenuto, il packager inserisce `skd:` URL nel manifesto M3U8. Dopo il `skd:` , è possibile inserire qualsiasi dato nel manifesto. Puoi utilizzare questi dati nel codice dell’applicazione per completare le attività elencate in precedenza. Ad esempio, puoi utilizzare `skd:{content_id}` in modo che l’app possa determinare l’ID del contenuto riprodotto e richiedere un token per quello specifico contenuto. Ad esempio, puoi utilizzare `skd:{entitlement_server_url}?cid={content_id}`, in modo che l&#39;app non debba avere l&#39;URL del server dei diritti codificato.

Potresti non aver bisogno di informazioni nel tuo `skd:` URL se, all’avvio della riproduzione, conosci già l’ID contenuto tramite altri canali. Il secondo esempio è la soluzione ideale per testare la configurazione, ma puoi utilizzarla anche in un ambiente di produzione.

>[!TIP]
>
>È possibile determinare il formato di `skd:`.

Il contenuto viene ottenuto utilizzando `skd:` ma la richiesta di licenza utilizza `https:`. Le opzioni più comuni per gestire questi protocolli sono:

* **Test iniziale della riproduzione end-to-end** Quando crei il pacchetto del contenuto, seleziona una `skd:` URL. Durante il test dell&#39;app, acquisire manualmente una licenza da ExpressPlay e codificare la licenza (un `https:` URL) e l’URL del contenuto nel caricatore.

   Ad esempio:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **La maggior parte degli altri casi** Quando crei il pacchetto del contenuto, seleziona una `skd:` URL che rappresenta in modo univoco l’ID del contenuto. Nel caricatore, analizzare `skd:` URL, invialo al server per acquisire un token e utilizza il token risultante come URL.

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

## Abilitare Apple FairPlay nelle applicazioni TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Puoi implementare Apple FairPlay Streaming, la soluzione DRM di Apple, nelle applicazioni TVSDK.

1. Creare il programma FairPlay Customer Resource Loader implementando `PTAVAssetResourceLoaderDelegate`.

   Per ulteriori informazioni, consulta [Apple FairPlay nelle applicazioni TVSDK](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Accertati di seguire le istruzioni riportate nella sezione *Guida al programma di streaming FairPlay* ( *FairPlayStreaming_PG.pdf*), incluso in [SDK del server FairPlay per lo sviluppo di un’app compatibile con FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Il `resourceLoader:shouldWaitForLoadingOfRequestedResource` il metodo equivale a quello in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Nello scenario del server di licenze ExpressPlay, per riprodurre il contenuto, modificare lo schema URL nell&#39;URL della richiesta di licenza del server ExpressPlay FairPlay da `skd://` a `https://` (o `https://`).

1. Registra il *FairPlay* Caricatore risorse cliente con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se si è creato il proprio server licenze FairPlay o si sta utilizzando un server licenze FairPlay di terze parti, consultare il fornitore del server licenze per determinare l&#39;URL del server licenze, la formattazione e altri requisiti.
