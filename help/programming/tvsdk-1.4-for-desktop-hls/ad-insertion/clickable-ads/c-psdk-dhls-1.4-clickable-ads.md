---
description: TVSDK fornisce informazioni utili per intervenire sugli annunci click-through. Quando crei la tua interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.
title: Annunci cliccabili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Annunci cliccabili {#clickable-ads}

TVSDK fornisce informazioni utili per intervenire sugli annunci click-through. Quando crei la tua interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.

Per TVSDK per Flash Runtime, è possibile fare clic solo sugli annunci lineari.

## Rispondi ai clic sugli annunci {#respond-to-clicks-on-ads}

Quando un utente fa clic su un annuncio o su un pulsante correlato, l&#39;applicazione è responsabile della risposta. TVSDK fornisce informazioni sull’URL di destinazione.

Questo esempio mostra un modo possibile per gestire i clic sugli annunci.

1. Ogni volta che viene riprodotto un annuncio, mostra un pulsante sul lettore multimediale. Un utente che fa clic sull&#39;annuncio viene reindirizzato all&#39;URL dell&#39;annuncio. Questo pulsante fa parte del [!DNL ClickableAdsOverlay.xml].

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

1. Includi questa sovrapposizione sul nostro esempio di lettore multimediale, [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Per rendere la visualizzazione visibile solo durante la riproduzione di un annuncio, ascolta gli eventi `onAdStart` e `onAdComplete` inviati da .

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

1. Monitora le interazioni degli utenti sugli annunci cliccabili. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, invia una notifica a TVSDK con `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Ascoltare l&#39;evento `AdclickEvent.AD_CLICK`.

   Se un annuncio è in riproduzione, TVSDK invia l&#39;evento `AdClickEvent.AD_CLICK` dal quale è possibile recuperare l&#39;URL di click-through e le relative informazioni.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Mette in pausa il lettore multimediale mentre indirizza l&#39;utente all&#39;URL dell&#39;annuncio.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Visualizza l&#39;URL di click-through dell&#39;annuncio e tutte le informazioni correlate.

       Ad esempio, puoi visualizzarlo in uno dei seguenti modi:
   
   * Apri l’URL di click-through in un browser all’interno dell’applicazione.

      Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene in genere utilizzata per richiamare URL click-through quando l’utente fa clic.
   * Reindirizza l’utente al browser web per dispositivi mobili esterno.

      Sui dispositivi mobili, l’area di riproduzione degli annunci video viene utilizzata per altre funzioni, ad esempio per nascondere e visualizzare i controlli, mettere in pausa la riproduzione, espandere a schermo intero e così via. Pertanto, sui dispositivi mobili, una visualizzazione separata, ad esempio un pulsante di sponsorizzazione, viene solitamente presentata all’utente come mezzo per avviare l’URL di click-through.

1. Chiudi la finestra del browser in cui vengono visualizzate le informazioni relative al click-through e riprende la riproduzione del video.
