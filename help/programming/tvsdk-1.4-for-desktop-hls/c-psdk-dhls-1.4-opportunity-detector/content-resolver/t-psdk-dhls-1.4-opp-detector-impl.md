---
description: È possibile implementare rilevatori di opportunità personalizzati.
seo-description: È possibile implementare rilevatori di opportunità personalizzati.
seo-title: Implementare un rilevatore di opportunità personalizzato
title: Implementare un rilevatore di opportunità personalizzato
uuid: 18fb431b-4585-4293-92a7-b77ab7f9b7db
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Implementa un rilevatore di opportunità personalizzato{#implement-a-custom-opportunity-detector}

È possibile implementare rilevatori di opportunità personalizzati.

* Se il generatore di opportunità è basato su `TimedMetadata` oggetti associati al flusso multimediale corrente, deve estendere il `SpliceOutOpportunityGenerator` o `TimedMetadataOpportunityGenerator`.

* Se il generatore di opportunità è basato su dati fuori banda forniti da un servizio esterno (ad esempio un CIS), è necessario estendere il `OpportunityGenerator`.

1. Crea il generatore di opportunità personalizzato.

       Se il generatore di opportunità personalizzato è basato su oggetti &quot;TimedMetadata&quot;, espandi il generatore `TimedMetadataOpportunityGenerator` e sostituisci i seguenti metodi:
   
   * `doConfigure` - Questo metodo viene chiamato dopo la creazione dell&#39;elemento del lettore multimediale e fornisce al generatore di opportunità di creare una serie iniziale di opportunità, se necessario
   * `doProcess` - Questo metodo viene chiamato ogni volta che  `TimedMetadata` viene rilevato un nuovo evento (ad esempio, per flussi live/lineari ogni volta che la playlist o gli aggiornamenti del manifesto)

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

1. Create il content factory personalizzato, che utilizza il generatore di opportunità personalizzato.

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

