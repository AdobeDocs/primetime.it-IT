---
description: TVSDK fornisce informazioni che consentono di agire sugli annunci click-through. Quando crei l’interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.
title: Annunci cliccabili
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Annunci cliccabili {#clickable-ads}

TVSDK fornisce informazioni che consentono di agire sugli annunci click-through. Quando crei l’interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.

Per TVSDK per Flash Runtime, è possibile fare clic solo sugli annunci lineari.

## Rispondi ai clic sugli annunci {#respond-to-clicks-on-ads}

Quando un utente fa clic su un annuncio o su un pulsante correlato, l’applicazione è responsabile della risposta. TVSDK fornisce informazioni sull’URL di destinazione.

Questo esempio mostra un modo possibile per gestire i clic sugli annunci.

1. Ogni volta che viene riprodotto un annuncio, visualizza un pulsante sopra il lettore multimediale. L’utente che fa clic sull’annuncio viene reindirizzato all’URL dell’annuncio. Questo pulsante fa parte del [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. Includi questa sovrapposizione nell’esempio del lettore multimediale, [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Per rendere visibile la visualizzazione solo durante la riproduzione di un annuncio, ascolta `onAdStart` e `onAdComplete` eventi inviati da .

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. Monitora le interazioni degli utenti sugli annunci cliccabili. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, notifica a TVSDK `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Ascolta la `AdclickEvent.AD_CLICK` evento.

   Se un annuncio è in riproduzione, TVSDK invia `AdClickEvent.AD_CLICK` , da cui è possibile recuperare l&#39;URL di click-through e le informazioni correlate.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Metti in pausa il lettore multimediale mentre indirizzi l’utente all’URL dell’annuncio.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Visualizza l’URL di click-through dell’annuncio ed eventuali informazioni correlate.

       Ad esempio, puoi visualizzarlo in uno dei seguenti modi:
   
   * Apri l’URL di click-through in un browser all’interno dell’applicazione.

     Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene generalmente utilizzata per richiamare gli URL di click-through quando l’utente fa clic su di essa.
   * Reindirizza l’utente al browser web mobile esterno.

     Sui dispositivi mobili, l’area di riproduzione e il video vengono utilizzati per altre funzioni, ad esempio per nascondere e visualizzare i controlli, mettere in pausa la riproduzione, espandersi a schermo intero e così via. Pertanto, sui dispositivi mobili, una visualizzazione separata, ad esempio un pulsante di sponsor, viene solitamente presentata all’utente come mezzo per avviare l’URL di click-through.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riprendete la riproduzione del video.
