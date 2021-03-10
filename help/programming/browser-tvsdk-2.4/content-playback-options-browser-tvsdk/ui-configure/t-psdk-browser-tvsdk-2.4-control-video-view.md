---
description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView .
title: Controllare la posizione e le dimensioni della visualizzazione video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Controllare la posizione e le dimensioni della visualizzazione video{#control-the-position-and-size-of-the-video-view}

È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l&#39;oggetto MediaPlayerView .

Il browser TVSDK per impostazione predefinita tenta di mantenere le proporzioni della visualizzazione video ogni volta che le dimensioni o la posizione del video vengono modificate a causa di una modifica apportata dall’applicazione, di un interruttore di profilo, di un interruttore di contenuto e così via.

È possibile ignorare il comportamento predefinito delle proporzioni specificando un diverso *criterio di scalabilità*. Specificare il criterio di scalabilità utilizzando la proprietà `scalePolicy` dell&#39;oggetto `MediaPlayerView`. Il criterio di scalabilità predefinito di `MediaPlayerView` viene impostato con un&#39;istanza della classe `MaintainAspectRatioScalePolicy`. Per reimpostare il criterio di scalabilità, sostituisci l’istanza predefinita di `MaintainAspectRatioScalePolicy` su `MediaPlayerView.scalePolicy` con il tuo criterio.

>[!IMPORTANT]
>
>Non è possibile impostare la proprietà `scalePolicy` su un valore null.

## Scenari di fallback non Flash {#non-flash-fallback-scenarios}

In scenari di fallback non Flash, affinché il criterio di scalabilità funzioni correttamente, l’elemento div video fornito nel costruttore `View` deve restituire valori diversi da zero per `offsetWidth` e `offsetHeight`. Per fornire un esempio di funzione errata, a volte quando la larghezza e l’altezza degli elementi div del video non sono impostate esplicitamente in css, il costruttore `View` restituisce zero per `offsetWidth` o `offsetHeight`.

>[!NOTE]
>
>Il supporto di CustomScalePolicy è limitato per alcuni browser, in particolare IE, Edge e Safari 9. Per questi browser, le proporzioni native del video non possono essere modificate. Tuttavia, la posizione e le dimensioni del video saranno applicate in base alla politica di scala.

1. Implementa l&#39;interfaccia `MediaPlayerViewScalePolicy` per creare criteri di scalabilità personalizzati.

   Il `MediaPlayerViewScalePolicy` dispone di un metodo:

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

1. Assegna l&#39;implementazione alla proprietà `MediaPlayerView` .

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Aggiungi la visualizzazione alla proprietà `view` di Media Player.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Ad esempio: Adatta il video a tutto il video, senza mantenere le proporzioni:**

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

