---
description: Puoi implementare i tuoi rilevatori di opportunità implementando l’interfaccia PlacementOpportunityDetector.
title: Implementare un rilevatore di opportunità personalizzato
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementare un rilevatore di opportunità personalizzato {#implement-a-custom-opportunity-detector}

Puoi implementare i tuoi rilevatori di opportunità implementando l’interfaccia PlacementOpportunityDetector.

1. Creare un `AdvertisingFactory` istanza e sostituzione `createOpportunityDetector`. Ad esempio:

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

1. Registra la factory dell’ad client su `MediaPlayer`. Ad esempio:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Creare una classe di rilevamento opportunità personalizzata che estenda `PlacementOpportunityDetector` classe.
   1. Nel rilevatore opportunità personalizzato, sostituisci questa funzione:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      Il `timedMetadataList` contiene l&#39;elenco di `TimedMetadata`, che è ordinato. I metadati contengono i parametri di targeting e i parametri personalizzati da inviare al provider di annunci.

   1. Per ogni `TimedMetadata`, crea un `List<PlacementOpportunity>`. L’elenco può essere vuoto, ma non nullo. `PlacementOpportunity` deve avere i seguenti attributi:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Dopo aver creato le opportunità di posizionamento per tutti gli oggetti metadati temporizzati rilevati, è sufficiente restituire `PlacementOpportunity` elenco.

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
