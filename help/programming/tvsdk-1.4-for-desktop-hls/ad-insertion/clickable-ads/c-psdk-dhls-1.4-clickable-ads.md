---
description: TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.
seo-description: TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.
seo-title: Annunci cliccabili
title: Annunci cliccabili
uuid: edefbc66-2d30-441d-9c30-256588504463
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Annunci cliccabili {#clickable-ads}

TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.

Per TVSDK per Runtime Flash, è possibile fare clic solo sugli annunci lineari.

## Rispondi ai clic sugli annunci {#respond-to-clicks-on-ads}

Quando un utente fa clic su un annuncio o su un pulsante correlato, l&#39;applicazione risponde. TVSDK fornisce informazioni sull’URL di destinazione.

In questo esempio viene illustrato un modo possibile per gestire i clic degli annunci.

1. Ogni volta che viene riprodotto un annuncio, viene visualizzato un pulsante sul lettore multimediale. Un utente che fa clic sull’annuncio viene reindirizzato all’URL dell’annuncio. Questo pulsante fa parte del [!DNL ClickableAdsOverlay.xml].

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

1. Includete questa sovrapposizione nell&#39;esempio di lettore multimediale [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Per rendere la visualizzazione visibile solo durante la riproduzione di un annuncio, ascoltare gli eventi `onAdStart` e `onAdComplete` inviati da .

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

1. Monitora le interazioni degli utenti sugli annunci cliccabili. Quando l&#39;utente tocca o fa clic sull&#39;annuncio o sul pulsante, invia una notifica a TVSDK con `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Ascoltare l&#39;evento `AdclickEvent.AD_CLICK`.

   Se viene riprodotto un annuncio, TVSDK invia l&#39;evento `AdClickEvent.AD_CLICK` dal quale è possibile recuperare l&#39;URL click-through e le informazioni correlate.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Metti in pausa il lettore multimediale mentre indirizza l&#39;utente all&#39;URL dell&#39;annuncio.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Visualizza l&#39;URL di click-through dell&#39;annuncio e tutte le informazioni correlate.

       Ad esempio, potete visualizzarlo in uno dei seguenti modi:
   
   * Aprite l’URL di click-through in un browser all’interno dell’applicazione.

      Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene in genere utilizzata per richiamare gli URL di click-through quando l’utente fa clic su di essi.
   * Reindirizzare l’utente al browser Web esterno per dispositivi mobili.

      Sui dispositivi mobili, l’area di riproduzione video e video è utilizzata per altre funzioni, come nascondere e mostrare i controlli, mettere in pausa la riproduzione, espandere la visualizzazione a schermo intero e così via. Di conseguenza, sui dispositivi mobili, una vista separata, come un pulsante di sponsorizzazione, viene in genere presentata all’utente come mezzo per avviare l’URL di click-through.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riavviate la riproduzione del video.
