---
description: Puoi implementare dei resolver di contenuto personalizzati in base ai resolver predefiniti.
title: Implementare un sistema di risoluzione dei contenuti personalizzato
exl-id: 04eff874-8a18-42f0-adb2-5b563e5c6a31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Implementare un sistema di risoluzione dei contenuti personalizzato {#implement-a-custom-content-resolver}

Puoi implementare dei resolver di contenuto personalizzati in base ai resolver predefiniti.

Quando TVSDK genera una nuova opportunità, scorre attraverso i risolutori di contenuti registrati alla ricerca di una che sia in grado di risolvere tale opportunità. Il primo che restituisce `true` è selezionato per risolvere l’opportunità. Se non è in grado di risolvere i contenuti, tale opportunità viene saltata. Poiché il processo di risoluzione dei contenuti è in genere asincrono, il resolver dei contenuti è responsabile della notifica a TVSDK al termine del processo.

1. Implementare `ContentFactory`, estendendo la `ContentFactory` interfaccia e sostituzione `retrieveResolvers`.

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

1. Registra il `ContentFactory` al `MediaPlayer`.

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

1. Passa un `AdvertisingMetadata` a TVSDK come segue:
   1. Creare un `AdvertisingMetadata` oggetto.
   1. Salva il `AdvertisingMetadata` oggetto a `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. Creare una classe ad resolver personalizzata che estenda `ContentResolver` classe.
   1. Nel resolver dell’annuncio personalizzato, sostituisci `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      Ottieni il tuo `advertisingMetadata` dall&#39;elemento passato `doConfigure`:

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

   1. Dopo la risoluzione degli annunci, chiama una delle seguenti funzioni:

      * Se la risoluzione dell’annuncio ha esito positivo, chiama `process(List<TimelineOperation> proposals)` e `notifyCompleted(Opportunity opportunity)` il `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * Se la risoluzione dell’annuncio non riesce, chiama `notifyResolveError` il `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         Ad esempio:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

Questo esempio di risolutore di annunci personalizzato risolve un’opportunità e fornisce un annuncio semplice:

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
