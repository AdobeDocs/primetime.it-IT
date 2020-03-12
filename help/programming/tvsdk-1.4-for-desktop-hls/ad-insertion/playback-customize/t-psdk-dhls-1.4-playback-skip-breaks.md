---
description: Per impostazione predefinita, TVSDK forza la riproduzione di un'interruzione di annuncio quando l'utente cerca su un'interruzione di annuncio. Potete personalizzare il comportamento per saltare un'interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.
seo-description: Per impostazione predefinita, TVSDK forza la riproduzione di un'interruzione di annuncio quando l'utente cerca su un'interruzione di annuncio. Potete personalizzare il comportamento per saltare un'interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.
seo-title: Ignora interruzioni annuncio per un periodo di tempo
title: Ignora interruzioni annuncio per un periodo di tempo
uuid: 1a18d5fd-c957-481b-83ae-2129590c1678
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ignora interruzioni annuncio per un periodo di tempo{#skip-ad-breaks-for-a-period-of-time}

Per impostazione predefinita, TVSDK forza la riproduzione di un&#39;interruzione di annuncio quando l&#39;utente cerca su un&#39;interruzione di annuncio. Potete personalizzare il comportamento per saltare un&#39;interruzione annuncio se il tempo trascorso da un completamento interruzione precedente è compreso entro un certo numero di minuti.

>[!IMPORTANT]
>
>Quando viene eseguito un tentativo interno di saltare un annuncio, potrebbe verificarsi una leggera pausa nella riproduzione.

L&#39;esempio seguente di un selettore di criteri di pubblicità personalizzato salta gli annunci nei prossimi cinque minuti (ora dell&#39;orologio a muro) dopo che un utente ha visto un&#39;interruzione di annuncio.

1. Estendi il selettore di criteri di annunci predefinito per ignorare il comportamento predefinito.

   ```
   /** 
    * Custom ad policy selector. 
    */ 
   public class CustomAdPolicySelector extends DefaultAdPolicySelector { 
   
       /** 
        * Default constructor. 
        * 
        * @param item Associated media player item. 
        */ 
       public function CustomAdPolicySelector(item:MediaPlayerItem) { 
           super(item); 
   
           item.player.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED,  
                                        onAdBreakCompleted); 
       } 
   
       override public function selectPolicyForAdBreak(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForAdBreak(adPolicyInfo); 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       override public function selectAdBreaksToPlay(adPolicyInfo:AdPolicyInfo):Vector.<AdBreakTimelineItem> { 
           if (shouldPlayAds()) { 
               return super.selectAdBreaksToPlay(adPolicyInfo); 
           } 
   
           return new Vector.<AdBreakTimelineItem>(); 
       } 
   
       override public function selectPolicyForSeekIntoAd(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForSeekIntoAd(adPolicyInfo); 
           } 
   
           return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
       } 
   
       private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
           _lastAdBreakPlayedTime = new Date().valueOf(); 
       } 
   
       private function shouldPlayAds():Boolean { 
           var currentTime:Number = new Date().valueOf(); 
           return isNaN(_lastAdBreakPlayedTime) 
                   ||  (currentTime - _lastAdBreakPlayedTime > _minimumInterval); 
       } 
   
       private var _lastAdBreakPlayedTime:Number = NaN; 
       private var _minimumInterval:Number = 300000; // 5 minutes in milliseconds 
   }
   ```

1. Create una nuova factory pubblicitaria che utilizzi il vostro selettore personalizzato.

   ```
   public class CustomAdPolicyContentFactory extends DefaultContentFactory { 
   
       private var _adPolicySelector:CustomAdPolicySelector; 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomAdPolicyContentFactory() { 
   
       } 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
       if (!_adPolicySelector) { 
           _adPolicySelector = new CustomAdPolicySelector(item); 
       } 
   
       return _adPolicySelector; 
       } 
   }
   ```

1. Registrare la nuova classe di annunci pubblicitari da utilizzare con MediaPlayer.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

