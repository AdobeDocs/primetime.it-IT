---
description: È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l'oggetto MediaPlayerView.
title: Controlla la posizione e le dimensioni della visualizzazione video
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Controlla la posizione e le dimensioni della visualizzazione video{#control-the-position-and-size-of-the-video-view}

È possibile controllare la posizione e le dimensioni della visualizzazione video utilizzando l&#39;oggetto MediaPlayerView.

Per impostazione predefinita, il browser TVSDK tenta di mantenere le proporzioni della visualizzazione video ogni volta che la dimensione o la posizione del video cambia a causa di una modifica apportata dall’applicazione, da un interruttore di profilo, da un interruttore di contenuto e così via.

È possibile ignorare il comportamento predefinito delle proporzioni specificando un *criteri di scalabilità*. Specificare il criterio di scalabilità utilizzando `MediaPlayerView` dell&#39;oggetto `scalePolicy` proprietà. Criterio di scala predefinito di `MediaPlayerView` è impostato con un&#39;istanza di `MaintainAspectRatioScalePolicy` classe. Per reimpostare il criterio di scalabilità, sostituire l&#39;istanza predefinita di `MaintainAspectRatioScalePolicy` il `MediaPlayerView.scalePolicy` con la tua politica.

>[!IMPORTANT]
>
>Impossibile impostare `scalePolicy` su un valore null.

## Scenari di fallback non di Flash {#non-flash-fallback-scenarios}

In scenari di fallback non di Flash, affinché i criteri di scala funzionino correttamente, l’elemento div video fornito in `View` il costruttore deve restituire valori diversi da zero per `offsetWidth` e `offsetHeight`. Per fare un esempio di funzione non corretta, a volte quando la larghezza e l&#39;altezza degli elementi div video non sono impostate esplicitamente in css, allora il `View` costruttore restituisce zero per `offsetWidth` o `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy dispone di supporto limitato per alcuni browser, in particolare IE, Edge e Safari 9. Per questi browser, le proporzioni native del video non possono essere modificate. Tuttavia, la posizione e le dimensioni del video verranno applicate in base alla politica di scala.

1. Implementare `MediaPlayerViewScalePolicy` per creare criteri di scalabilità personalizzati.

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

1. Assegna l’implementazione a `MediaPlayerView` proprietà.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Aggiungere la visualizzazione al lettore multimediale `view` proprietà.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**Ad esempio: ridimensiona il video per riempire l’intera visualizzazione video, senza mantenere le proporzioni:**

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
