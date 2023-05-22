---
description: Per impostazione predefinita, TVSDK forza la riproduzione di un’interruzione pubblicitaria quando l’utente cerca sopra un’interruzione pubblicitaria. Puoi personalizzare il comportamento per saltare un’interruzione pubblicitaria se il tempo trascorso dal completamento di un’interruzione precedente è entro un determinato numero di minuti.
title: Ignorare le interruzioni pubblicitarie per un periodo di tempo
exl-id: 7d5ee788-4a67-4c70-acc7-a950e6b2db8a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Ignorare le interruzioni pubblicitarie per un periodo di tempo{#skip-ad-breaks-for-a-period-of-time}

Per impostazione predefinita, TVSDK forza la riproduzione di un’interruzione pubblicitaria quando l’utente cerca sopra un’interruzione pubblicitaria. Puoi personalizzare il comportamento per saltare un’interruzione pubblicitaria se il tempo trascorso dal completamento di un’interruzione precedente è entro un determinato numero di minuti.

>[!IMPORTANT]
>
>Quando è presente una ricerca interna per saltare un annuncio, potrebbe essere presente una leggera pausa nella riproduzione.

L’esempio seguente di selettore di criteri di annuncio personalizzato ignora gli annunci nei successivi cinque minuti (tempo di clock a parete) dopo che un utente ha guardato un’interruzione pubblicitaria.

1. Estendi il selettore dei criteri degli annunci predefinito per ignorare il comportamento predefinito.

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

1. Crea una nuova advertising factory che utilizza il selettore personalizzato.

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

1. Registrare la nuova classe di fabbrica pubblicitaria da utilizzare con MediaPlayer.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
