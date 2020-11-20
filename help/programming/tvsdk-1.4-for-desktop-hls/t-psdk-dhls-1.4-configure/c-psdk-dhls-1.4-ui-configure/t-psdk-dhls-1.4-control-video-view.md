---
description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView.
seo-description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView.
seo-title: Controllare la posizione e le dimensioni della visualizzazione video
title: Controllare la posizione e le dimensioni della visualizzazione video
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Controllare la posizione e le dimensioni della visualizzazione video{#control-the-position-and-size-of-the-video-view}

È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l&#39;oggetto MediaPlayerView.

Per impostazione predefinita, TVSDK tenta di mantenere le proporzioni della visualizzazione video ogni volta che la dimensione o la posizione del video cambia (a causa di una modifica apportata dall’applicazione, da un interruttore di profilo, da uno switch di contenuto, ecc.).

Potete ignorare il comportamento predefinito delle proporzioni specificando un criterio *di* scala diverso. Specificare il criterio di scala utilizzando la proprietà dell&#39; `MediaPlayerView` oggetto `scalePolicy` . Il criterio di scala `MediaPlayerView`predefinito è impostato con un&#39;istanza della `MaintainAspectRatioScalePolicy` classe. Per ripristinare il criterio di scala, sostituite l&#39;istanza predefinita di `MaintainAspectRatioScalePolicy` on `MediaPlayerView.scalePolicy` con il criterio personalizzato. Non è possibile impostare la `scalePolicy` proprietà su un valore null.

1. Implementate l&#39; `MediaPlayerViewScalePolicy` interfaccia per creare un criterio di scala personalizzato.

   È `MediaPlayerViewScalePolicy` disponibile un metodo:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK utilizza un `StageVideo` oggetto per visualizzare il video, e poiché `StageVideo` gli oggetti non sono nell&#39;elenco di visualizzazione, il `viewPort` parametro contiene le coordinate assolute del video.
   >
   >
   >Ad esempio:
   >
   >```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```

1. Assegnare l&#39;implementazione alla `MediaPlayerView` proprietà.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Aggiungere la visualizzazione alla `view` proprietà di Media Player.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Ad esempio: Adatta il video per riempire l’intera visualizzazione video, senza mantenere le proporzioni:**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```

