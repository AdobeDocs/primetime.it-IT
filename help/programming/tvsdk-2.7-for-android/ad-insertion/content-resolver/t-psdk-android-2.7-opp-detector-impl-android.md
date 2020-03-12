---
description: Potete implementare i generatori di opportunità personalizzati implementando la classe OpportunityGenerator.
seo-description: Potete implementare i generatori di opportunità personalizzati implementando la classe OpportunityGenerator.
seo-title: Implementazione di un generatore di opportunità personalizzato
title: Implementazione di un generatore di opportunità personalizzato
uuid: 93d8253f-10f9-4950-a273-28975cb69caa
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Implementazione di un generatore di opportunità personalizzato {#implement-a-custom-opportunity-generator}

Potete implementare i generatori di opportunità personalizzati implementando la classe OpportunityGenerator.

1. Implementate la vostra personalizzazione `ContentFactory` implementando l&#39; `ContentFactory` interfaccia e sostituendo `retrieveGenerators`.

   Ad esempio:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
           List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
           generators.add(MyOpportunityGenerator(item)); 
           return generators; 
       } 
       ... 
   }
   ```

1. Registra il `ContentFactory` file nel `MediaPlayer`.

   Ad esempio:

   ```java
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Creare una classe di generatore di opportunità personalizzata che implementa la `OpportunityGenerator` classe.

   ```java
   public class CustomOpportunityGenerator implements OpportunityGenerator  
   {...}
   ```

   1. Nel generatore di opportunità personalizzato, sostituisci `doConfigure`, `doUpdate` e `doCleanup`:

      ```java
      @Override 
       public void configure(MediaPlayerItem item, Context context,  
       OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
      
      protected void update(long playhead, TimeRange playbackRange){ 
      } 
      
      protected void cleanup(){ 
      }
      ```

      Per ottenere i metadati temporizzati:

      ```java
      List<TimedMetadata> tList = getItem().getTimedMetadata(); 
      ```

   1. Per ciascun `TimedMetadata` o gruppo di `TimedMetadata`, create un&#39;opportunità con i seguenti attributi:

      ```java
      Opportunity( 
        String id,                      // Can be id from timedMetadata  
        Placement placementInformation, // Placement object containing Type, time, duration 
        Metadata metadataSettings,      // Ad metadata with targeting params sent to the ad provider 
        Metadata customParams           // Metadata for customizing resolving and/or tracking process. 
      ); 
      ```

   1. Per ogni opportunità creata, chiama `resolve` il `OpportunityGeneratorClient:getClient().resolve(opportunity);`.

<!--<a id="example_7A46377EBE79458E87423EB95D0568D4"></a>-->

Questo è un esempio di rilevatore di opportunità di posizionamento personalizzato:

```java
public class MyOpportunityGenerator implements OpportunityGenerator {

     @Override 
      public void configure(MediaPlayerItem item, Context context,  
      OpportunityGeneratorClient client, AdSignalingMode mode, long playhead, TimeRange playbackRange) { 
      } 
 
        MediaPlayerItem item = getItem(); 
        MediaPlayerItemConfig itemConfig = item.getConfig(); 
 
        if (itemConfig == null || itemConfig.getAdvertisingMetadata() == null) { 
            // no ad metadata, no ads 
            return; 
        } 
 
        AdvertisingMetadata metadata = item.getConfig().getAdvertisingMetadata();

        AdSignalingMode mode = itemConfig.getAdSignalingMode(); 
 
        if (mode == AdSignalingMode.CUSTOM_RANGES) 
        { 
            // don't override custom ad ranges 
            return; 
        } 
 
        Placement.Type pType = (mode == AdSignalingMode.MANIFEST_CUES) ?  
                  Placement.Type.PRE_ROLL : Placement.Type.SERVER_MAP; 
        Placement.Mode pMode = Placement.Mode.DEFAULT; 
        Placement placement = new Placement(pType, playhead,  
                  Placement.UNKNOWN_DURATION, pMode); 
 
        Opportunity opportunity = new Opportunity("initialOpportunity", placement,  
                  metadata, null); 
 
        OpportunityGeneratorClient client = getClient(); 
        client.resolve(opportunity); 
    } 
 
    @Override 
    protected void update(long playhead, TimeRange playbackRange) { 
 
 ... 
 timedMetadataList = getItem().getTimedMetadata(); 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
         if (isOpportunity(timedMetadata)) {   // check if given timedMetadata should  
                                               // be considered as an opportunity 
  // create a PlacementOpportunity object and add it to the opportunities list 
                Opportunity opportunity = new Opportunity("id", placement, metadata, null); 
                client.resolve(opportunity) 
          } 
        } 
    } 
 
    @Override 
    protected void cleanup() {} 
}
```

