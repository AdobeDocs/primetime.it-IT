---
description: È possibile implementare i resolver in base ai resolver predefiniti.
title: Implementare un risolutore di opportunità/contenuti personalizzato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Implementa un risolutore di opportunità/contenuti personalizzato {#implement-a-custom-opportunity-content-resolver}

È possibile implementare i resolver in base ai resolver predefiniti.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Sviluppa un risolutore di annunci personalizzato estendendo la classe astratta `PTContentResolver` .

   `PTContentResolver` è un&#39;interfaccia che deve essere implementata da una classe content resolver. È disponibile anche una classe astratta con lo stesso nome e gestisce automaticamente la configurazione (ottenendo il delegato).

   >[!TIP]
   >
   >`PTContentResolver` è esposto attraverso la  `PTDefaultMediaPlayerClientFactory` classe . I clienti possono registrare un nuovo risolutore di contenuti estendendo la classe astratta `PTContentResolver` . Per impostazione predefinita, e a meno che non sia stato rimosso in modo specifico, un `PTDefaultAdContentResolver` viene registrato in `PTDefaultMediaPlayerClientFactory`.

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

1. Implementa `shouldResolveOpportunity` e restituisce `YES` se deve gestire il `PTPlacementOpportunity` ricevuto.
1. Implementa `resolvePlacementOpportunity`, che inizia a caricare il contenuto alternativo o gli annunci.
1. Dopo aver caricato gli annunci, prepara un `PTTimeline` con le informazioni sul contenuto da inserire.

       Seguono alcune utili informazioni sulle timeline:
   
   * Possono essere presenti più tipi `PTAdBreak`di pre-roll, mid-roll e post-roll.

      * A `PTAdBreak` ha i seguenti elementi:

         * A `CMTimeRange` con l&#39;ora di inizio e la durata dell&#39;interruzione.

            Viene impostata come proprietà di intervallo di `PTAdBreak`.

         * `NSArray` di  `PTAd`s.

            Viene impostata come proprietà degli annunci di `PTAdBreak`.
   * Un `PTAd` rappresenta l&#39;annuncio e ogni `PTAd` ha i seguenti elementi:

      * Un `PTAdHLSAsset` impostato come proprietà della risorsa principale dell’annuncio.
      * Possibilità di più istanze `PTAdAsset` come annunci cliccabili o banner pubblicitari.

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

1. Chiama `didFinishResolvingPlacementOpportunity`, che fornisce il `PTTimeline`.
1. Registra il tuo rivenditore di contenuti/annunci personalizzati nella fabbrica del lettore multimediale predefinita chiamando `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Se hai implementato un risolutore di opportunità personalizzato, registralo nella fabbrica predefinita del lettore multimediale.

   >[!TIP]
   >
   >Non è necessario registrare un risolutore di opportunità personalizzato per registrare un risolutore di contenuti/annunci personalizzato.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

Quando il lettore carica il contenuto ed è determinato come di tipo VOD o LIVE, si verifica una delle seguenti situazioni:

* Se il contenuto è VOD, viene utilizzato il risolutore di contenuto personalizzato per ottenere la timeline dell’annuncio dell’intero video.
* Se il contenuto è LIVE, il risolutore di contenuto personalizzato viene chiamato ogni volta che viene rilevata un’opportunità di posizionamento (punto di cue) nel contenuto.