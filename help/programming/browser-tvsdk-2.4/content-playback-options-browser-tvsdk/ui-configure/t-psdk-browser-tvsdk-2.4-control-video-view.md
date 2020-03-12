---
description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView.
seo-description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView.
seo-title: Controllare la posizione e le dimensioni della visualizzazione video
title: Controllare la posizione e le dimensioni della visualizzazione video
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Controllare la posizione e le dimensioni della visualizzazione video{#control-the-position-and-size-of-the-video-view}

È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l&#39;oggetto MediaPlayerView.

Per impostazione predefinita, il browser TVSDK tenta di mantenere le proporzioni della visualizzazione video ogni volta che le dimensioni o la posizione del video vengono modificate a causa di una modifica apportata dall’applicazione, un interruttore del profilo, uno switch del contenuto e così via.

Potete ignorare il comportamento predefinito delle proporzioni specificando un criterio *di* scala diverso. Specificare il criterio di scala utilizzando la proprietà dell&#39; `MediaPlayerView` oggetto `scalePolicy` . Il criterio di scala predefinito di `MediaPlayerView` è impostato con un&#39;istanza della `MaintainAspectRatioScalePolicy` classe. Per ripristinare il criterio di scala, sostituite l&#39;istanza predefinita di `MaintainAspectRatioScalePolicy` on `MediaPlayerView.scalePolicy` con il criterio personalizzato.

>[!IMPORTANT]
>
>Non è possibile impostare la `scalePolicy` proprietà su un valore null.

## Scenari di fallback non Flash {#non-flash-fallback-scenarios}

Negli scenari di fallback non Flash, affinché il criterio di ridimensionamento funzioni correttamente, l&#39;elemento div video fornito nel `View` costruttore deve restituire valori diversi da zero per `offsetWidth` e `offsetHeight`. Per fornire un esempio di funzione non corretta, talvolta quando la larghezza e l&#39;altezza degli elementi div video non sono impostate esplicitamente in css, il `View` costruttore restituisce zero per `offsetWidth` o `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy dispone di un supporto limitato per alcuni browser, in particolare IE, Edge e Safari 9. Per questi browser, non è possibile modificare le proporzioni native del video. Tuttavia, la posizione e le dimensioni del video verranno applicate in base ai criteri di ridimensionamento.

1. Implementate l&#39; `MediaPlayerViewScalePolicy` interfaccia per creare un criterio di scala personalizzato.

   È `MediaPlayerViewScalePolicy` disponibile un metodo:

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   Ad esempio:

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. Assegnare l&#39;implementazione alla `MediaPlayerView` proprietà.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Aggiungere la visualizzazione alla `view` proprietà di Media Player.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Ad esempio: Adatta il video per riempire l’intera visualizzazione video, senza mantenere le proporzioni:**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```

