---
description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView .
title: Controllare la posizione e le dimensioni della visualizzazione video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Controllare la posizione e le dimensioni della visualizzazione video{#control-the-position-and-size-of-the-video-view}

È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l&#39;oggetto MediaPlayerView .

Per impostazione predefinita, TVSDK tenta di mantenere le proporzioni della visualizzazione video ogni volta che la dimensione o la posizione del video cambia (a causa di una modifica apportata dall’applicazione, da un interruttore di profilo, da un interruttore di contenuto, ecc.).

È possibile ignorare il comportamento predefinito delle proporzioni specificando un diverso *criterio di scalabilità*. Specificare il criterio di scalabilità utilizzando la proprietà `scalePolicy` dell&#39;oggetto `MediaPlayerView`. Il criterio di scalabilità predefinito di `MediaPlayerView` viene impostato con un&#39;istanza della classe `MaintainAspectRatioScalePolicy`. Per reimpostare il criterio di scalabilità, sostituisci l’istanza predefinita di `MaintainAspectRatioScalePolicy` su `MediaPlayerView.scalePolicy` con il tuo criterio. (Non è possibile impostare la proprietà `scalePolicy` su un valore null.)

1. Implementa l&#39;interfaccia `MediaPlayerViewScalePolicy` per creare criteri di scalabilità personalizzati.

   Il `MediaPlayerViewScalePolicy` dispone di un metodo:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK utilizza un oggetto `StageVideo` per la visualizzazione del video e, poiché gli oggetti `StageVideo` non sono nell’elenco di visualizzazione, il parametro `viewPort` contiene le coordinate assolute del video.
   >
   >
   >Ad esempio:
   >
   >
   ```
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

1. Assegna l&#39;implementazione alla proprietà `MediaPlayerView` .

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Aggiungi la visualizzazione alla proprietà `view` di Media Player.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Ad esempio: Adatta il video a tutto il video, senza mantenere le proporzioni:**

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

