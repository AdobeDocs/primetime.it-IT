---
description: TVSDK supporta la visualizzazione di annunci lineari VPAID (Video Player-Ad Interface Definition) in un'interruzione pubblicitaria. La versione 1.0 di VPAID richiede Flash, mentre la versione 2.0 funziona anche con il browser TVSDK e JavaScript.
title: Visualizzare annunci VPAID lineari in un'interruzione pubblicitaria
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Visualizza annunci VPAID lineari in un&#39;interruzione pubblicitaria{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK supporta la visualizzazione di annunci lineari VPAID (Video Player-Ad Interface Definition) in un&#39;interruzione pubblicitaria. La versione 1.0 di VPAID richiede Flash, mentre la versione 2.0 funziona anche con il browser TVSDK e JavaScript.

Per visualizzare correttamente gli annunci VPAID, devi fornire un contenitore di annunci ( `AdContainerView`) all&#39;interno dell&#39;istanza `MediaPlayerContext`.

Limitazioni per gli annunci VPAID:

* Gli annunci VPAID non hanno necessariamente una durata predefinita, dato che l&#39;annuncio può essere interattivo. Pertanto, la durata dell&#39;annuncio (definita dalla risposta dell&#39;ad server) potrebbe non corrispondere sempre esattamente alla durata effettiva dell&#39;annuncio.
* Per gli annunci VPAID 1.0, TVSDK richiede Flash Player 14.0.0.160 o versione successiva installato sul dispositivo. Per le versioni precedenti del lettore di Flash, questa funzione è disabilitata e gli annunci VPAID 1.0 vengono saltati.

Per impostare un contenitore di annunci per la visualizzazione di annunci VPAID (versione 1.0 o 2.0) all’interno di un’interruzione di pubblicità:

1. Utilizza il seguente codice di esempio per impostare un contenitore di annunci che possa mostrare annunci VPAID.

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

1. Quando la visualizzazione viene ridimensionata, reimposta la dimensione sul contenitore dell’annuncio.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Quando ricevi un evento di modifica a schermo intero e imposti le nuove dimensioni sul contenitore dell’annuncio, passa lo stato di visualizzazione dell’area di visualizzazione come segue per garantire che il lettore venga ridimensionato correttamente:
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

