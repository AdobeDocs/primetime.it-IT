---
description: È possibile implementare i propri risolutori di contenuti in base ai risolutori predefiniti.
title: Implementare un risolutore di contenuti personalizzato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---


# Implementa un risolutore di contenuti personalizzato {#implement-a-custom-content-resolver}

È possibile implementare i propri risolutori di contenuti in base ai risolutori predefiniti.

Quando TVSDK genera una nuova opportunità, esegue un’iterazione attraverso i risolutori di contenuti registrati alla ricerca di una in grado di risolvere tale opportunità. Il primo che restituisce `true` viene selezionato per risolvere l&#39;opportunità. Se nessun risolutore di contenuti è in grado, tale opportunità viene ignorata. Poiché il processo di risoluzione dei contenuti è in genere asincrono, il risolutore dei contenuti è responsabile della notifica a TVSDK al termine del processo.

1. Implementa il tuo `ContentFactory` personalizzato, estendendo l&#39;interfaccia `ContentFactory` e ignorando `retrieveResolvers`.

   Ad esempio:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. Registra il `ContentFactory` nel `MediaPlayer`.

   Ad esempio:

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Passa un oggetto `AdvertisingMetadata` a TVSDK come segue:
   1. Creare un oggetto `AdvertisingMetadata`.
   1. Salvare l’oggetto `AdvertisingMetadata` su `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. Crea una classe ad resolver personalizzata che estende la classe `ContentResolver` .
   1. Nel risolutore di annunci personalizzato, sovrascrivi `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      Ottieni il tuo `advertisingMetadata` dall&#39;elemento trasmesso in `doConfigure`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. Per ogni opportunità di posizionamento, crea un `List<TimelineOperation>`.

      Questo esempio `TimelineOperation` fornisce una struttura per `AdBreakPlacement`:

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. Una volta risolti gli annunci, chiama una delle seguenti funzioni:

      * Se la risoluzione dell&#39;annuncio ha esito positivo, chiama `process(List<TimelineOperation> proposals)` e `notifyCompleted(Opportunity opportunity)` sul`ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * Se la risoluzione dell&#39;annuncio non riesce, chiama `notifyResolveError` su `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         Ad esempio:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

Questo ad resolver personalizzato di esempio risolve un&#39;opportunità e fornisce un annuncio semplice:

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

