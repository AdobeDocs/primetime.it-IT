---
description: È possibile implementare i propri risolutori di contenuti in base ai risolutori predefiniti.
title: Implementare un risolutore di contenuti personalizzato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 1%

---


# Implementa un risolutore di contenuti personalizzato{#implement-a-custom-content-resolver}

È possibile implementare i propri risolutori di contenuti in base ai risolutori predefiniti.

Quando il browser TVSDK rileva una nuova opportunità, esegue un&#39;iterazione attraverso i risolutori di contenuti registrati alla ricerca di una che sia in grado di risolvere tale opportunità utilizzando il metodo `canResolve` . Il primo che restituisce true viene selezionato per risolvere l&#39;opportunità. Se nessun risolutore di contenuti è in grado di farlo, questa opportunità viene ignorata. Poiché il processo di risoluzione dei contenuti è in genere asincrono, il risolutore dei contenuti è responsabile della notifica al browser TVSDK al termine del processo.

Ricorda le seguenti informazioni:

* Il risolutore dei contenuti chiama `client.process` per specificare quale operazione timeline deve essere eseguita da TVSDK.

   L’operazione di solito è un posizionamento di interruzione annuncio.

* Il risolutore dei contenuti chiama `client.notifyCompleted` se il processo di risoluzione ha esito positivo o `client.notifyFailed` se il processo non riesce.

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

1. Crea la content factory personalizzata che utilizza il risolutore di contenuti personalizzato.

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

   Nel lettore di framework dell&#39;interfaccia utente, puoi specificare una directory di fabbrica del contenuto personalizzata come segue:

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

