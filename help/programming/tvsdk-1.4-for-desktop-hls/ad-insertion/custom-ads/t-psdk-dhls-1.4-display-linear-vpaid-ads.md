---
description: TVSDK supporta la visualizzazione di annunci VPAID (Video Player-Ad Interface Definition) lineari in un'interruzione di pubblicità. La versione 1.0 di VPAID richiede Flash, mentre la versione 2.0 funziona anche con l'SDK per browser e JavaScript.
seo-description: TVSDK supporta la visualizzazione di annunci VPAID (Video Player-Ad Interface Definition) lineari in un'interruzione di pubblicità. La versione 1.0 di VPAID richiede Flash, mentre la versione 2.0 funziona anche con l'SDK per browser e JavaScript.
seo-title: Visualizzare annunci VPAID lineari in un'interruzione annuncio
title: Visualizzare annunci VPAID lineari in un'interruzione annuncio
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Visualizzare annunci VPAID lineari in un&#39;interruzione annuncio{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK supporta la visualizzazione di annunci VPAID (Video Player-Ad Interface Definition) lineari in un&#39;interruzione di pubblicità. La versione 1.0 di VPAID richiede Flash, mentre la versione 2.0 funziona anche con l&#39;SDK per browser e JavaScript.

Per visualizzare correttamente gli annunci VPAID, devi fornire un contenitore di annunci ( `AdContainerView`) all&#39;interno dell&#39; `MediaPlayerContext` istanza.

Limitazioni per gli annunci VPAID:

* Gli annunci VPAID non hanno necessariamente una durata predefinita, dato che l&#39;annuncio può essere interattivo. Di conseguenza, la durata dell&#39;annuncio (definita dalla risposta del server di annunci) potrebbe non corrispondere sempre esattamente alla durata effettiva dell&#39;annuncio.
* Per gli annunci VPAID 1.0, TVSDK richiede Flash Player 14.0.0.160 o versione successiva installato sul dispositivo. Per le versioni precedenti del lettore Flash, questa funzione è disabilitata e gli annunci VPAID 1.0 vengono ignorati.

Per impostare un contenitore di annunci per la visualizzazione di annunci VPAID (versione 1.0 o 2.0) all&#39;interno di un&#39;interruzione di annuncio:

1. Utilizzate il seguente codice di esempio per impostare un contenitore di annunci che possa mostrare annunci VPAID.

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. Quando la vista viene ridimensionata, reimpostate la dimensione sul contenitore degli annunci.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Quando si verifica un evento di modifica a schermo intero e si imposta la nuova dimensione sul contenitore degli annunci, passare lo stato di visualizzazione dell’area di visualizzazione come segue per garantire che il lettore venga ridimensionato correttamente:    >
   >
   >
   ```>
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```   >
   >



