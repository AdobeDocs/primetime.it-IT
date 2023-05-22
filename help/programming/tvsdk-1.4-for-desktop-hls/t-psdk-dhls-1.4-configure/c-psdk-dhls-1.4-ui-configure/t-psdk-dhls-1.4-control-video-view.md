---
description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView.
title: Controlla la posizione e le dimensioni della visualizzazione video
exl-id: 5e7ae557-7f2b-4697-85eb-e72d1f43a7fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Controlla la posizione e le dimensioni della visualizzazione video{#control-the-position-and-size-of-the-video-view}

È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l&#39;oggetto MediaPlayerView.

Per impostazione predefinita, TVSDK tenta di mantenere le proporzioni della visualizzazione video ogni volta che la dimensione o la posizione del video cambia (a causa di una modifica apportata dall’applicazione, da un interruttore di profilo, da un interruttore di contenuto, ecc.).

È possibile ignorare il comportamento predefinito delle proporzioni specificando un *criteri di scalabilità*. Specificare il criterio di scalabilità utilizzando `MediaPlayerView` dell&#39;oggetto `scalePolicy` proprietà. Il `MediaPlayerView`Il criterio di scala predefinito è impostato con un&#39;istanza del `MaintainAspectRatioScalePolicy` classe. Per reimpostare il criterio di scalabilità, sostituire l&#39;istanza predefinita di `MaintainAspectRatioScalePolicy` il `MediaPlayerView.scalePolicy` con la tua politica. (Impossibile impostare `scalePolicy` a un valore nullo.)

1. Implementare `MediaPlayerViewScalePolicy` per creare criteri di scalabilità personalizzati.

   Il `MediaPlayerViewScalePolicy` dispone di un metodo:

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK utilizza un `StageVideo` oggetto per la visualizzazione del video e perché `StageVideo` non sono presenti nell&#39;elenco di visualizzazione, `viewPort` Il parametro contiene le coordinate assolute del video.
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

1. Assegna l’implementazione a `MediaPlayerView` proprietà.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Aggiungere la visualizzazione al lettore multimediale `view` proprietà.

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**Ad esempio: ridimensiona il video per riempire l’intera visualizzazione video, senza mantenere le proporzioni:**

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
