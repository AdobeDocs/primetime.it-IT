---
description: Potete implementare il vostro generatore di opportunità estendendo l'interfaccia OpportunityGenerator.
seo-description: Potete implementare il vostro generatore di opportunità estendendo l'interfaccia OpportunityGenerator.
seo-title: Implementazione di un generatore di opportunità personalizzato
title: Implementazione di un generatore di opportunità personalizzato
uuid: b80da2da-32d5-41f7-86ca-936d6f25b015
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 4%

---


# Implementare un generatore di opportunità personalizzato{#implement-a-custom-opportunity-generator}

Potete implementare il vostro generatore di opportunità estendendo l&#39;interfaccia OpportunityGenerator.

1. Crea il generatore di opportunità personalizzato.

   Ad esempio:

   ```js
   /** 
   * Class implementing AdobePSDK.OpportunityGenerator interface 
   */ 
   CustomOpportunityGenerator = function () { 
   }; 
   
   CustomOpportunityGenerator.prototype = { 
       constructor: CustomOpportunityGenerator, 
       configureCallbackFunc: function (item, client, mode, playhead, playbackRange) {  
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current AdobePSDK.MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadatas = item.timedMetadata; 
       }, 
       updateCallbackFunc: function (playhead, playbackRange) { 
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve (opportunity); 
       }, 
       … 
   }; 
   ```

1. Create il content factory personalizzato, che utilizza il generatore di opportunità personalizzato.

   Ad esempio:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
          constructor: CustomContentFactory, 
          retrieveOpportunityGeneratorsCallbackFunc: function (item) { 
               var result = []; 
               result.push (new CustomOpportunityGenerator()); 
               return result; 
       }, 
       … 
   }; 
   ```

1. Registra il content factory personalizzato per il flusso multimediale da riprodurre.

   In UI Framework Player è possibile specificare una content factory personalizzata nel modo seguente:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
           mediaPlayerItemConfig: { 
                   advertisingFactory: advertisingFactory 
           }, 
               mediaResource: { 
                   resourceUrl:'Specify Resource Url' 
          } 
     } 
   }); 
   ```

