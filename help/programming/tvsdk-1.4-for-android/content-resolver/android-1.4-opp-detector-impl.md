---
description: Puoi implementare i tuoi rilevatori di opportunità implementando l’interfaccia PlacementOpportunityDetector.
seo-description: Puoi implementare i tuoi rilevatori di opportunità implementando l’interfaccia PlacementOpportunityDetector.
seo-title: Implementare un rilevatore di opportunità personalizzato
title: Implementare un rilevatore di opportunità personalizzato
uuid: 012527c5-4ef0-4cd6-a9df-2fb861078a7e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 2%

---


# Implementare un rilevatore di opportunità personalizzato {#implement-a-custom-opportunity-detector}

Puoi implementare i tuoi rilevatori di opportunità implementando l’interfaccia PlacementOpportunityDetector.

1. Create un&#39;istanza `AdvertisingFactory` personalizzata ed eseguite l&#39;override di `createOpportunityDetector`. Ad esempio:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. Registra il produttore del client di annunci in `MediaPlayer`. Ad esempio:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Create una classe di rilevamento opportunità personalizzata che estenda la classe `PlacementOpportunityDetector`.
   1. Nel rilevatore di opportunità personalizzato, sostituisci questa funzione:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      Il `timedMetadataList` contiene l&#39;elenco di `TimedMetadata` disponibili, ordinato. I metadati contengono i parametri di targeting e i parametri personalizzati da inviare al provider di annunci.

   1. Per ogni `TimedMetadata`, create un `List<PlacementOpportunity>`. L&#39;elenco può essere vuoto, ma non nullo. `PlacementOpportunity` devono avere i seguenti attributi:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Dopo aver creato opportunità di posizionamento per tutti gli oggetti metadati temporizzati rilevati, è sufficiente restituire l&#39;elenco `PlacementOpportunity`.

Questo è un esempio di rilevatore di opportunità di posizionamento personalizzato:

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```

