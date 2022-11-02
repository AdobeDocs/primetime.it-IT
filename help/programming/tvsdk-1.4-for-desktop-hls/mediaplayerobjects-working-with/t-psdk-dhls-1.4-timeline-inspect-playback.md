---
description: Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.
title: Inspect la timeline di riproduzione
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Inspect la timeline di riproduzione{#inspect-the-playback-timeline}

Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.

Ecco un esempio di implementazione, come mostrato nella schermata successiva.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. Accedere al `Timeline` nell&#39;oggetto `MediaPlayer` utilizzando `get` metodo .

   La `Timeline` incapsula le informazioni correlate al contenuto della timeline associata all&#39;elemento multimediale attualmente caricato dal `MediaPlayer` istanza. La `Timeline` La classe fornisce l&#39;accesso a una visualizzazione in sola lettura della timeline sottostante. La `Timeline` Classe fornisce un metodo getter per ottenere tutti gli elementi inseriti `TimelineMarker` oggetti.

1. Itera attraverso l&#39;elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

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
