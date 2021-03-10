---
description: Puoi implementare i tuoi rilevatori di opportunità implementando l'interfaccia PlacementOpportunityDetector (Rilevatore opportunità).
title: Implementare un rilevatore di opportunità personalizzato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# Implementa un rilevatore di opportunità personalizzato {#implement-a-custom-opportunity-detector}

Puoi implementare i tuoi rilevatori di opportunità implementando l&#39;interfaccia PlacementOpportunityDetector (Rilevatore opportunità).

1. Crea un&#39;istanza `AdvertisingFactory` personalizzata e sovrascrivi `createOpportunityDetector`. Ad esempio:

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

1. Registra la Ad Client Factory in `MediaPlayer`. Ad esempio:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Crea una classe di rilevatore di opportunità personalizzata che estende la classe `PlacementOpportunityDetector` .
   1. Nel rilevatore di opportunità personalizzato, sovrascrivi questa funzione:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      Il `timedMetadataList` contiene l&#39;elenco di disponibili `TimedMetadata`, ordinato. I metadati contengono i parametri di targeting e i parametri personalizzati da inviare al provider di annunci.

   1. Per ogni `TimedMetadata`, crea un `List<PlacementOpportunity>`. L’elenco può essere vuoto, ma non nullo. `PlacementOpportunity` devono avere i seguenti attributi:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Dopo aver creato opportunità di posizionamento per tutti gli oggetti metadati temporizzati rilevati, è sufficiente restituire l&#39; `PlacementOpportunity` elenco.

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

