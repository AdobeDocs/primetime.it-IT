---
description: Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.
seo-description: Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.
seo-title: Implementazione di un risolutore di contenuti personalizzato
title: Implementazione di un risolutore di contenuti personalizzato
uuid: 1714fcd9-45e0-48be-97f3-f702265128a4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementazione di un risolutore di contenuti personalizzato{#implement-a-custom-content-resolver}

Potete implementare dei risolutori di contenuti personalizzati in base ai risolutori predefiniti.

Quando TVSDK rileva una nuova opportunità, esegue un&#39;iterazione attraverso i risolutori di contenuto registrati alla ricerca di una che sia in grado di risolvere tale opportunità utilizzando il `canResolve` metodo . Il primo che restituisce true è selezionato per la risoluzione dell&#39;opportunità. Se non è in grado di risolvere il problema, tale opportunità viene ignorata. Poiché il processo di risoluzione del contenuto è in genere asincrono, il risolutore del contenuto è responsabile della notifica a TVSDK al termine del processo.

* Il risolutore dei contenuti richiama `client.place` per specificare quale operazione timeline deve essere eseguita TVSDK (in genere un posizionamento di interruzione annuncio).
* Il risolutore del contenuto chiama `client.notifyCompleted` se il processo di risoluzione ha esito positivo o `client.notifyFailed` se il processo ha esito negativo.

1. Crea un risolutore di opportunità personalizzato.

   ```
   public class CustomResolver extends ContentResolver { 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomResolver() { 
       } 
   
       override protected function doConfigure(item:MediaPlayerItem):void { 
           // here you can read any media stream characteristics which 
           // might help configure your content resolver like 
           // - the media player item configuration through the item.config 
           // - the media resource metadata through item.resource.metadata 
       } 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function doCanResolve(opportunity:Opportunity):Boolean { 
           // check if the opportunity can be resolved by this resolver 
           // if yes return true, otherwise return false 
   
           return true; 
       } 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function doResolve(opportunity:Opportunity):void { 
           // start the resolving process 
           // communicate with your custom ad server 
   
           // in this example we assume that: 
           // - if successful, onResolveCompleted method will be invoked 
           // - if failed, onResolveFailed method will be invoked 
       } 
   
       private function onResolveCompleted(response:*):void { 
           try { 
               var proposals:Vector.<TimelineOperation> = new Vector.<TimelineOperation>(); 
   
               // extract the timeline ad placement from the response 
               // and add them to the proposal vector 
               // - extract the ad break 
               // - calculate the placement ( can reuse the opportunity.placement ) 
               // var timelineOperation:AdBreakPlacement = new AdBreakPlacement(placement, adBreak); 
               // proposals.push(timelineOperation); 
   
               client.process(proposals); 
               client.notifyCompleted(_opportunity); 
           } catch (error:Error) { 
               onResolveFailed(error); 
           } 
       } 
   
       private function onResolveFailed(error:Error):void { 
   
           var errorMetadata:Metadata = new Metadata(); 
           MetadataUtils.serializeError(error, errorMetadata); 
   
           var mediaError:MediaError = new MediaError(NotificationCode.CONTENT_RESOLVING_ERROR, errorMetadata); 
           client.notifyFailed(_opportunity, mediaError); 
       } 
   
       ... 
   }
   ```

1. Create la content factory personalizzata, che utilizza il risolutore di contenuti personalizzato.

   Ad esempio:

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
           ... 
   
           /** 
            * @inheritDoc 
            */ 
           override protected function  
             doRetrieveResolvers(item:MediaPlayerItem):Vector.<ContentResolver> { 
               var result:Vector.<ContentResolver> = new Vector.<ContentResolver>(); 
   
               var resource:MediaResource = item.resource; 
   
               if (resource.metadata != null) { 
                   if (resource.metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY)) { 
                       result.push(new AuditudeAdResolver()); 
                   } else if (resource.metadata.containsKey("custom-opportunity-detector")) { 
                       result.push(new CustomResolver()); 
                   } 
               } 
               return result; 
           } 
   }
   ```

1. Registra il content factory personalizzato per il flusso multimediale da riprodurre.

   Ad esempio:

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   var advertisingMetadata:AdvertisingMetadata = new AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue("customparam", "customvalue"); 
   
   var metadata:Metadata = new Metadata(); 
   metadata.setMetadata("custom-opportunity-detector", advertisingMetadata); 
   var mediaResource:MediaResource = MediaResource.createFromUrl(url, metadata);
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

