---
description: Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo barra di scorrimento personalizzato in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.
title: Inspect la timeline di riproduzione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect la timeline di riproduzione{#inspect-the-playback-timeline}

Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo barra di scorrimento personalizzato in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.

Di seguito è riportato un esempio di implementazione, come mostrato nella schermata seguente.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. Accedere a `Timeline` oggetto in `MediaPlayer` utilizzando `get` metodo.

   Il `Timeline` La classe incapsula le informazioni correlate al contenuto della timeline associata all&#39;elemento multimediale attualmente caricato da `MediaPlayer` dell&#39;istanza. Il `Timeline` La classe consente di accedere a una visualizzazione di sola lettura della timeline sottostante. Il `Timeline` La classe fornisce un metodo getter per ottenere tutti gli elementi posizionati `TimelineMarker` oggetti.

1. Scorrere l&#39;elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

       Un oggetto &quot;TimelineMarker&quot; contiene due informazioni:
   
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
