---
description: Puoi implementare i tuoi rilevatori di opportunità.
title: Implementare un rilevatore di opportunità personalizzato
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Implementare un rilevatore di opportunità personalizzato{#implement-a-custom-opportunity-detector}

Puoi implementare i tuoi rilevatori di opportunità.

* Se il generatore di opportunità si basa su `TimedMetadata` associati al flusso multimediale corrente, quindi deve estendere il `SpliceOutOpportunityGenerator` o `TimedMetadataOpportunityGenerator`.

* Se il generatore di opportunità si basa su dati fuori banda forniti da un servizio esterno (ad esempio un CIS), deve estendere il `OpportunityGenerator`.

1. Crea il generatore di opportunità personalizzato.

       Se il generatore di opportunità personalizzato si basa su oggetti &quot;TimedMetadata&quot;, estendi &quot;TimedMetadataOpportunityGenerator&quot; ed esegui l’override di questi metodi:
   
   * `doConfigure` : questo metodo viene richiamato dopo la creazione dell’elemento del lettore multimediale e, se necessario, fornisce al generatore di opportunità la possibilità di creare un set iniziale di opportunità
   * `doProcess` - Questo metodo viene chiamato ogni volta che si verifica una nuova `TimedMetadata` viene rilevato (ad esempio, per flussi live/lineari ogni volta che la playlist/manifesto si aggiorna)

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

1. Crea il factory dei contenuti personalizzato, che utilizza il generatore di opportunità personalizzato.

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

1. Registra il factory dei contenuti personalizzati per il flusso multimediale da riprodurre.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
