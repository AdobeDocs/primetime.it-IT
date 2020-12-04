---
description: Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.
seo-description: Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.
seo-title: Implementazione di un risolutore di contenuti personalizzato
title: Implementazione di un risolutore di contenuti personalizzato
uuid: cf85dd90-242e-4f9e-9785-158ca0fc9465
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Implementazione di un risolutore di contenuto personalizzato{#implement-a-custom-content-resolver}

Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.

Quando l&#39;SDK per browser rileva una nuova opportunità, esegue un&#39;iterazione attraverso i risolutori di contenuti registrati alla ricerca di una in grado di risolvere tale opportunità utilizzando il metodo `canResolve`. Il primo che restituisce true è selezionato per la risoluzione dell&#39;opportunità. Se non è in grado di risolvere il problema, tale opportunità viene ignorata. Poiché il processo di risoluzione del contenuto è in genere asincrono, il risolutore del contenuto è responsabile della notifica a Browser TVSDK al termine del processo.

Ricorda le seguenti informazioni:

* Il risolutore del contenuto chiama `client.process` per specificare quale operazione timeline deve essere eseguita da TVSDK.

   In genere si tratta di un posizionamento di interruzione annuncio.

* Il risolutore del contenuto chiama `client.notifyCompleted` se il processo di risoluzione ha esito positivo o `client.notifyFailed` se il processo ha esito negativo.

1. Crea un risolutore di opportunità personalizzato.

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

1. Create la content factory personalizzata, che utilizza il risolutore di contenuti personalizzato.

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

1. Registra il content factory personalizzato per il flusso multimediale da riprodurre.

   Nel lettore UI Framework, potete specificare una content factory personalizzata nel modo seguente:

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

