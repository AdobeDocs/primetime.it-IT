---
description: Per impostazione predefinita, TVSDK forza la riproduzione di un'interruzione di annuncio quando l'utente cerca su un'interruzione di annuncio. Potete personalizzare il comportamento per saltare un'interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.
seo-description: Per impostazione predefinita, TVSDK forza la riproduzione di un'interruzione di annuncio quando l'utente cerca su un'interruzione di annuncio. Potete personalizzare il comportamento per saltare un'interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.
seo-title: Ignora interruzioni annuncio per un periodo di tempo
title: Ignora interruzioni annuncio per un periodo di tempo
uuid: f8a5c1e3-e97f-421f-ac98-79de94a82955
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Ignora interruzioni annuncio per un periodo di tempo {#skip-ad-breaks-for-a-period-of-time}

Per impostazione predefinita, TVSDK forza la riproduzione di un&#39;interruzione di annuncio quando l&#39;utente cerca su un&#39;interruzione di annuncio. Potete personalizzare il comportamento per saltare un&#39;interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.

>[!IMPORTANT]
>
>Se dovete completare una ricerca interna per perdonare un annuncio, potrebbe verificarsi una leggera pausa durante la riproduzione.

Per ignorare il comportamento predefinito di TVSDK e interruzione, potete estendere il selettore predefinito dei criteri per gli annunci. Sono disponibili quattro criteri di interruzione annuncio:

* PLAY
* SKIP

   >[!NOTE]
   >
   >Il criterio SKIP per l&#39;interruzione degli annunci potrebbe non funzionare come previsto per i flussi in diretta quando un annuncio è presente in un punto attivo. Ad esempio, per un pre-roll, SKIP causerà una ricerca alla fine dell&#39;interruzione dell&#39;annuncio, che potrebbe essere maggiore del punto attivo. In questo caso, TVSDK potrebbe cercare al centro di un annuncio.

* REMOVE_AFTER
* RIMUOVI

   >[!NOTE]
   >
   >Il criterio di `REMOVE` interruzione annuncio è impostato come obsoleto. Adobe consiglia di utilizzare il criterio di `SKIP` interruzione annuncio al posto di `REMOVE`.

L&#39;esempio seguente di un selettore di criteri di pubblicità personalizzato salta gli annunci nei prossimi cinque minuti (ora dell&#39;orologio a muro) dopo che un utente ha visto un&#39;interruzione di annuncio.

1. Quando l&#39;utente ha terminato di guardare un&#39;interruzione annuncio, salva l&#39;ora del sistema corrente.

   ```java
   @Override 
   public void onAdBreakComplete(AdBreak adBreak) { 
       ... 
       if (isShouldPlayUpcomingAdBreakRuleEnabled()) { 
           CustomAdPolicySelector.setLastAdBreakPlayedTime(System.currentTimeMillis()); 
           ... 
       } 
   }
   ```

1. Estendi `AdPolicySelector`.

   ```java
   package com.adobe.mediacore.sample.advertising; 
   
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerItemConfig; 
   import com.adobe.mediacore.timeline.advertising.policy.*; 
   import com.adobe.mediacore.timeline.advertising.AdBreakTimelineItem; 
   import com.adobe.mediacore.metadata.AdvertisingMetadata; 
   
   import java.util.ArrayList; 
   import java.util.List; 
   
   public class CustomAdPolicySelector implements AdPolicySelector { 
   
       private static final long MIN_BREAK_INTERVAL = 300000; // 5 minutes for next ad break to be played 
       private MediaPlayerItem _mediaPlayerItem; 
       private static long _lastAdBreakPlayedTime; 
       private AdBreakWatchedPolicy watchedPolicy = AdBreakWatchedPolicy.WATCHED_ON_BEGIN; 
   
       public CustomAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           _mediaPlayerItem = mediaPlayerItem; 
           _lastAdBreakPlayedTime = 0; 
   
           if (mediaPlayerItem != null) { 
               watchedPolicy = extractWatchedPolicy(mediaPlayerItem.getConfig()); 
           } 
       } 
   
       @Override 
       public AdBreakPolicy selectPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
           if (shouldPlayAdBreaks() && adPolicyInfo.getAdBreakTimelineItems() != null) { 
   
               AdBreakTimelineItem item = adPolicyInfo.getAdBreakTimelineItems().get(0); 
   
               // This condition will remove the pre-roll ad from live stream after watching 
               if (item.getTime() == 0 && _mediaPlayerItem.isLive()) { 
                   return AdBreakPolicy.REMOVE_AFTER_PLAY; 
               } 
               if (item.getTime() == 0) { 
                   return AdBreakPolicy.PLAY; 
               } 
   
               // This condition will remove every ad break that has been watched once.  
               // Comment this section if you want to play watched ad breaks again. 
               if (item.isWatched()) { 
                   return AdBreakPolicy.SKIP; 
               } 
   
               return AdBreakPolicy.REMOVE_AFTER_PLAY; 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       @Override 
       public List<AdBreakTimelineItem> selectAdBreaksToPlay(AdPolicyInfo adPolicyInfo) { 
   
           if (shouldPlayAdBreaks()) { 
   
               List<AdBreakTimelineItem> timelineItems = adPolicyInfo.getAdBreakTimelineItems(); 
               AdBreakTimelineItem item; 
               List<AdBreakTimelineItem> selectedItems = new ArrayList<AdBreakTimelineItem>(); 
   
               if (timelineItems != null && timelineItems.size() > 0) { 
   
                   // Seek Forward Condition 
                   if (adPolicyInfo.getCurrentTime() <= adPolicyInfo.getSeekToTime()) { 
                       item = timelineItems.get(0); 
   
                       // Resume logic - This will be helpful in resuming the content  
                       // from last saved playback session, and just play the pre-roll ad 
                       if(adPolicyInfo.getCurrentTime() == 0) { 
                           if(item.getTime() == 0 && !item.isWatched()) { 
                               // comment this line if you just need to seek to the user's  
                               // last known position without playing pre-roll ad. ZD#820 
                               selectedItems.add(item); 
                               return selectedItems; 
                           } 
                           else{ 
                               return null; 
                           } 
                       } else { 
                           item = timelineItems.get(timelineItems.size()-1); 
                           if (!item.isWatched()) { 
                               selectedItems.add(item); 
                               return selectedItems; 
                           } 
                       } 
   
                       // Seek backward condition 
                   } else if (adPolicyInfo.getCurrentTime() > adPolicyInfo.getSeekToTime()) { 
                       item = timelineItems.get(0); 
   
                       if(!item.isWatched()) { 
                           selectedItems.add(item); 
                           return selectedItems; 
                       } else { 
                           return null; 
                       } 
                   } 
               } 
           } 
           return null; 
       } 
   
       @Override 
       public AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo) { 
           // Simple Ad Policy selector 
           // if the first ad in the break was watched,  
           // skip to the next add after the seek position 
           // otherwise, play the ads in the break from the beginning 
   
           List<AdBreakTimelineItem> timelineItems = adPolicyInfo.getAdBreakTimelineItems(); 
           if (timelineItems != null && timelineItems.size() > 0) { 
               if (timelineItems.get(0).isWatched()) { 
                   return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
               } 
           } 
   
           // Resume play from the next ad in the break 
           return AdPolicy.PLAY_FROM_AD_BREAK_BEGIN; 
   
       } 
   
       @Override 
       public AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
           return watchedPolicy; 
       } 
   
       public static void setLastAdBreakPlayedTime(long lastAdBreakPlayedTime) { 
           _lastAdBreakPlayedTime = lastAdBreakPlayedTime; 
       } 
   
       private boolean shouldPlayAdBreaks() { 
           long currentTime = System.currentTimeMillis(); 
   
           if (_lastAdBreakPlayedTime <= 0) { 
               return true; 
           } 
   
           if (_lastAdBreakPlayedTime > 0 &&  
             (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) { 
               return true; 
           } 
   
           // return false for not playing Ad if this  
           // Ad occurs with 5 minutes of last Ad playback 
           return false; 
       } 
   
       private AdBreakWatchedPolicy extractWatchedPolicy(MediaPlayerItemConfig config) { 
           if (config != null) { 
               AdvertisingMetadata metadata = config.getAdvertisingMetadata(); 
               if (metadata != null) { 
                   return metadata.getAdBreakWatchedPolicy(); 
               } 
           } 
           return AdBreakWatchedPolicy.WATCHED_ON_BEGIN; 
       } 
   } 
   ```

