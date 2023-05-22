---
description: Puoi implementare i resolver in base a quelli predefiniti.
title: Implementare un’opportunità personalizzata/risolutore contenuti
exl-id: f2a8512f-9f6c-4fd9-8694-32132cddc7d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Implementare un’opportunità personalizzata/risolutore contenuti{#implement-a-custom-opportunity-content-resolver}

Puoi implementare i resolver in base a quelli predefiniti.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Sviluppare un ad resolver personalizzato estendendo la `PTContentResolver` classe astratta.

   `PTContentResolver` è un’interfaccia che deve essere implementata da una classe del resolver dei contenuti. È inoltre disponibile una classe astratta con lo stesso nome che gestisce automaticamente la configurazione (ottenendo il delegato).

   >[!TIP]
   >
   >`PTContentResolver` è esposto tramite `PTDefaultMediaPlayerClientFactory` classe. I client possono registrare un nuovo risolutore di contenuti estendendo il `PTContentResolver` classe astratta. Per impostazione predefinita, e a meno che non venga specificamente rimossa, `PTDefaultAdContentResolver` è registrato in `PTDefaultMediaPlayerClientFactory`.

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. Implementare `shouldResolveOpportunity` e ritorno `YES` se deve gestire il `PTPlacementOpportunity`.
1. Implementare `resolvePlacementOpportunity`, che inizia a caricare il contenuto o gli annunci alternativi.
1. Dopo il caricamento degli annunci, prepara un `PTTimeline` con le informazioni sul contenuto da inserire.

       Seguono alcune informazioni utili sulle timeline:
   
   * Ci possono essere più `PTAdBreak`s di tipi pre-roll, mid-roll e post-roll.

      * A `PTAdBreak` presenta le seguenti caratteristiche:

         * A `CMTimeRange` con l’ora di inizio e la durata dell’interruzione.

            Viene impostata come proprietà intervallo di `PTAdBreak`.

         * `NSArray` di `PTAd`s.

            Viene impostata come proprietà ads di `PTAdBreak`.
   * A `PTAd` rappresenta l’annuncio, e ogni `PTAd` presenta le seguenti caratteristiche:

      * A `PTAdHLSAsset` impostata come proprietà della risorsa principale dell’annuncio.
      * Possibilmente multipli `PTAdAsset` istanze come annunci selezionabili o banner pubblicitari.

   Ad esempio:

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. Chiamata `didFinishResolvingPlacementOpportunity`, che fornisce `PTTimeline`.
1. Registra il contenuto personalizzato/ad resolver nella fabbrica predefinita del lettore multimediale chiamando `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Se hai implementato un risolutore opportunità personalizzato, registralo nella fabbrica predefinita del lettore multimediale.

   >[!TIP]
   >
   >Non è necessario registrare un resolver di opportunità personalizzato per registrare un contenuto personalizzato o un resolver di annunci.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

Quando il lettore carica il contenuto e viene determinato che è di tipo VOD o LIVE, si verifica una delle seguenti situazioni: >
* Se il contenuto è VOD, il risolutore contenuto personalizzato viene utilizzato per ottenere la timeline dell’annuncio dell’intero video.
* Se il contenuto è LIVE, il resolver del contenuto personalizzato viene chiamato ogni volta che nel contenuto viene rilevata un’opportunità di posizionamento (punto di cue).
