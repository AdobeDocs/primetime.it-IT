---
description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-title: Controllare la timeline di riproduzione
title: Controllare la timeline di riproduzione
uuid: 2f903493-2d88-4af2-ac71-36300b49735b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Controllare la timeline di riproduzione{#inspect-the-playback-timeline}

È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l&#39;applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell&#39;annuncio.

Di seguito è riportato un esempio di implementazione come mostrato nella schermata seguente.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Accedere all&#39; `Timeline` &#39;oggetto nel `MediaPlayer` metodo utilizzando il `get` .

   La `Timeline` classe racchiude le informazioni correlate al contenuto della cronologia associata all&#39;elemento multimediale attualmente caricato dall&#39; `MediaPlayer` istanza. La `Timeline` classe fornisce l&#39;accesso a una vista di sola lettura della timeline sottostante. La `Timeline` classe fornisce un metodo getter per ottenere tutti `TimelineMarker` gli oggetti posizionati.

1. Scorri l’elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

       Un oggetto `TimelineMarker` contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```

