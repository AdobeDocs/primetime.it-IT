---
description: Puoi implementare dei resolver di contenuto personalizzati in base ai resolver predefiniti.
title: Implementare un sistema di risoluzione dei contenuti personalizzato
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Implementare un sistema di risoluzione dei contenuti personalizzato{#implement-a-custom-content-resolver}

Puoi implementare dei resolver di contenuto personalizzati in base ai resolver predefiniti.

Quando il TVSDK del browser rileva una nuova opportunità, scorre attraverso i resolver di contenuti registrati alla ricerca di una che sia in grado di risolvere tale opportunità utilizzando `canResolve` metodo. Il primo che restituisce true viene selezionato per la risoluzione dell&#39;opportunità. Se non è possibile utilizzare alcun risolutore contenuti, tale opportunità viene ignorata. Poiché il processo di risoluzione dei contenuti è in genere asincrono, il resolver dei contenuti è responsabile della notifica a TVSDK del browser al termine del processo.

Tenere presenti le seguenti informazioni:

* Chiamate del resolver dei contenuti `client.process` per specificare l&#39;operazione della timeline da eseguire per TVSDK.

  L’operazione consiste solitamente nel posizionamento di un’interruzione pubblicitaria.

* Chiamate del resolver dei contenuti `client.notifyCompleted` se il processo di risoluzione ha esito positivo o `client.notifyFailed` se il processo non riesce.

1. Creare un risolutore opportunità personalizzato.

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
   
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
   
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
   
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
   
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
   
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
   
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
   
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
   
   }; 
   ```

1. Crea il factory dei contenuti personalizzato, che utilizza il risolutore contenuti personalizzato.

   Ad esempio:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   ```

1. Registra il factory dei contenuti personalizzati per il flusso multimediale da riprodurre.

   Nel lettore del framework dell’interfaccia utente, puoi specificare il factory dei contenuti personalizzato come segue:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
   
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
   
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
   
   }); 
   ```
