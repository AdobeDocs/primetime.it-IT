---
description: Potete abilitare un'esperienza simile a quella televisiva per partecipare nel mezzo di un annuncio, in streaming live.
seo-description: Potete abilitare un'esperienza simile a quella televisiva per partecipare nel mezzo di un annuncio, in streaming live.
seo-title: Inserimento interruzione annuncio parziale
title: Inserimento interruzione annuncio parziale
uuid: 296a9b6a-9e9f-4ca7-ab8a-c8cbc98fb9af
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inserimento interruzione annuncio parziale {#partial-ad-break-insertion}

Potete abilitare un&#39;esperienza simile a quella televisiva per partecipare nel mezzo di un annuncio, in streaming live.

La funzione di interruzione parziale degli annunci consente di riprodurre un&#39;esperienza simile a quella di un televisore in cui, se il cliente avvia uno streaming live all&#39;interno di un midroll, questo verrà avviato all&#39;interno di tale midrol. È simile al passaggio a un canale TV e la pubblicità funziona senza problemi.

Ad esempio, se un utente si unisce al centro di un annuncio pubblicitario di 90 secondi (tre annunci da 30 secondi), 10 secondi alla seconda pubblicità (ovvero, a 40 secondi dall&#39;interruzione dell&#39;annuncio), si verifica quanto segue:

* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
* I tracciatori di annunci per l&#39;annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Viene attivato solo il tracciatore del terzo annuncio.

Questo comportamento non è attivato per impostazione predefinita. Per abilitare questa funzione nell&#39;app, effettua le seguenti operazioni:

1. Disattivate i primi dinamici utilizzando il metodo setEnableLivePreroll della classe AdvertisingMetadata.

   ```
   advertisingMetadata.setEnableLivePreroll(String.valueOf(false))
   ```

1. Attivate la preferenza per l&#39;inserimento di interruzioni pubblicitarie parziali. Utilizzare il nuovo metodo setPartialAdBreakPref nell&#39;interfaccia di MediaPlayer per attivare questa funzione. Utilizzare il metodo getPartialAdBreakPref per trovare lo stato corrente di questa preferenza.

   ```
   MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
   
          mediaPlayer.setPartialAdBreakPref(true); 
   ```

1. Questa funzione richiede l&#39;implementazione di un selettore di criteri per gli annunci personalizzato per personalizzare il comportamento. Se non disponete già di un&#39;implementazione personalizzata della classe AdvertisingFactory, aggiungete una nuova implementazione AdvertisingFactory. Ignorare il metodo createAdPolicySelector. Questo metodo restituisce una nuova istanza dell&#39;implementazione di AdPolicySelector.

   Di seguito è riportata un&#39;implementazione di esempio per riferimento. L&#39;implementazione di esempio seguente è disponibile per l&#39;utilizzo dal pacchetto com.adobe.mediacore. Tuttavia, è semplificato per un riferimento semplice e non è consigliato utilizzarlo così com&#39;è.

   1. Selettore criteri annunci di esempio

      ```
       package com.adobe.mediacore;
      
      import com.adobe.mediacore.logging.Log; 
      import com.adobe.mediacore.logging.Logger; 
      import com.adobe.mediacore.metadata.*; 
      import com.adobe.mediacore.timeline.advertising.*; 
      
      import java.util.ArrayList; 
      import java.util.List; 
      
      public class PartialAdBreakAdPolicySelector implements AdPolicySelector { 
          private static final String LOG_TAG = "[PSDK]::" + DefaultAdPolicySelector.class.getSimpleName(); 
          private final Logger _logger = Log.getLogger(LOG_TAG); 
      
          private final MediaPlayerItem _mediaPlayerItem; 
          private final AdBreakAsWatched _adBreakAsWatchedPolicy; 
      
          public PartialAdBreakAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
              _mediaPlayerItem = mediaPlayerItem; 
              _adBreakAsWatchedPolicy = extractAdBreakAsWatchedPolicy(_mediaPlayerItem); 
          } 
      
          @Override 
          public AdBreakPolicy selectPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectPolicyForAdBreak", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              if (adPolicyInfo.getAdBreakPlacements().size() > 0) { 
                  AdBreakPlacement adBreakTimelineItem = adPolicyInfo.getAdBreakPlacements().get(0); 
                  if (adPolicyInfo.getMode() == AdPolicyMode.SEEK && adBreakTimelineItem.getAdBreak().isWatched()) { 
                      return AdBreakPolicy.SKIP; 
                  } 
              } 
      
              AdSignalingMode adSignalingMode = AdSignalingMode.DEFAULT; 
              if (_mediaPlayerItem != null) { 
                  MetadataNode metadata = (MetadataNode) _mediaPlayerItem.getResource().getMetadata(); 
                  if (metadata != null) { 
                      AdvertisingMetadata advertisingMetadata = (AdvertisingMetadata) metadata.getNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue()); 
                      if (advertisingMetadata != null) { 
                          adSignalingMode = advertisingMetadata.getSignalingMode(); 
                      } 
                  } 
              } 
      
              // can't remove main content due to a ave bug, need to check if stream is live or ad signaling mode is manifest cue 
              if (_mediaPlayerItem.isLive() || adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
                  return AdBreakPolicy.PLAY; 
              } 
      
              return AdBreakPolicy.REMOVE_AFTER_PLAY; 
          } 
      
          @Override 
          public List<AdBreakPlacement> selectAdBreaksToPlay(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectAdBreaksToPlay", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              List<AdBreakPlacement> adBreakPlacements = adPolicyInfo.getAdBreakPlacements(); 
              if (adBreakPlacements != null) { 
                  int size = adBreakPlacements.size(); 
                  List<AdBreakPlacement> adBreaks = new ArrayList<AdBreakPlacement>(); 
                  if (size > 0 && adPolicyInfo.getCurrentTime() <= adPolicyInfo.getSeekToTime()) { 
                      AdBreakPlacement adBreak = adBreakPlacements.get(size - 1); 
                      if (!adBreak.getAdBreak().isWatched()) { 
                          adBreaks.add(adBreak); 
                          return adBreaks; 
                      } 
                  } 
              } 
      
              return null; 
          } 
      
          @Override 
          public AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectPolicyForSeekIntoAd", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              // If you really want to allow seek during ads (you likely do not). 
              return AdPolicy.PLAY; 
          } 
      
          @Override 
          public AdBreakAsWatched selectWatchedPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
              _logger.i(LOG_TAG + "#selectWatchedPolicyForAdBreak", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                      + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
      
              return _adBreakAsWatchedPolicy; 
          } 
      
          /** 
           * Extract the ad break watched policy for the specified media player item. 
           * 
           * @param item Associated media player item. 
           * @return a valid ad break watched policy. 
           */ 
          private AdBreakAsWatched extractAdBreakAsWatchedPolicy(MediaPlayerItem item) { 
              AdBreakAsWatched adBreakWatchedPolicy = AdBreakAsWatched.AD_BREAK_AS_WATCHED_ON_BEGIN; 
      
              if (item != null) { 
                  MetadataNode metadata = (MetadataNode) item.getResource().getMetadata(); 
                  if (metadata != null) { 
                      AdvertisingMetadata advertisingMetadata = (AdvertisingMetadata) metadata.getNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue()); 
                      if (advertisingMetadata != null) { 
                          adBreakWatchedPolicy = advertisingMetadata.getAdBreakAsWatched(); 
                      } 
                  } 
              } 
      
              return adBreakWatchedPolicy; 
          } 
      } 
      ```

   1. Sample Advertising Factory

      ```
      private AdvertisingFactory createPartialAdBreakFactory() { 
      return new AdvertisingFactory() { 
      @Override 
                   public AdPolicySelector  
      createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
                      return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
                   } 
      
      // Rest of the interface methods can be overridden as per your  
      // customization needs 
      // As shown next 
      @Override 
      public AdPolicySelector  
      createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
         return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
        } 
      // . . . 
      
       } 
      } 
      ```

   1. Registrare la nostra AdvertisingFactory con il lettore multimediale

      ```
      AdvertisingFactory advertisingFactory = createPartialAdBreakFactory();  
      
      if (advertisingFactory != null) { 
                  mediaPlayer.registerAdClientFactory(advertisingFactory); 
      } 
      ```

   1. Ignorare il metodo createAdPolicySelector

      ```
      @Override 
      public AdPolicySelector  
      createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
         return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
      } 
      ```

