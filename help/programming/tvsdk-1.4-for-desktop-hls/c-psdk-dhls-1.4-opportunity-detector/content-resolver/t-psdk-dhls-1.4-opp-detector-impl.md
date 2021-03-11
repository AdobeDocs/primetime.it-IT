---
description: Puoi implementare i tuoi rilevatori di opportunità.
title: Implementare un rilevatore di opportunità personalizzato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Implementa un rilevatore di opportunità personalizzato{#implement-a-custom-opportunity-detector}

Puoi implementare i tuoi rilevatori di opportunità.

* Se il generatore di opportunità si basa su oggetti `TimedMetadata` associati al flusso multimediale corrente, deve estendere `SpliceOutOpportunityGenerator` o `TimedMetadataOpportunityGenerator`.

* Se il generatore di opportunità si basa su dati fuori banda forniti da un servizio esterno (ad esempio un CIS), deve estendere il `OpportunityGenerator`.

1. Crea il generatore di opportunità personalizzato.

       Se il generatore di opportunità personalizzato si basa su oggetti &quot;TimedMetadata&quot;, estendere l&#39;oggetto &quot;TimedMetadataOpportunityGenerator&quot; e ignorare questi metodi:
   
   * `doConfigure` - Questo metodo viene chiamato dopo la creazione dell&#39;elemento del lettore multimediale e fornisce al generatore di opportunità di creare un set iniziale di opportunità, se necessario
   * `doProcess` - Questo metodo viene chiamato ogni volta che  `TimedMetadata` viene rilevato un nuovo metodo (ad esempio, per flussi live/lineari ogni volta che la playlist/aggiornamento del manifesto)

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. Crea la content factory personalizzata, che utilizza il generatore di opportunità personalizzato.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. Registra il content factory personalizzato per il flusso multimediale da riprodurre.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

