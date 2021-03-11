---
description: Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.
title: Inspect la timeline di riproduzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect la timeline di riproduzione{#inspect-the-playback-timeline}

Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.

Ecco un esempio di implementazione, come mostrato nella schermata successiva.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Accedi all&#39;oggetto `Timeline` in `MediaPlayer` utilizzando il metodo `get` .

   La classe `Timeline` incapsula le informazioni correlate al contenuto della timeline associata all&#39;elemento multimediale attualmente caricato dall&#39;istanza `MediaPlayer`. La classe `Timeline` consente di accedere a una visualizzazione in sola lettura della timeline sottostante. La classe `Timeline` fornisce un metodo migliore per ottenere tutti gli oggetti `TimelineMarker` inseriti.

1. Itera l’elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

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

