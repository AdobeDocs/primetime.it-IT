---
description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-title: Controllare la timeline di riproduzione
title: Controllare la timeline di riproduzione
uuid: d5d68684-d658-44bc-bfff-952b7946c7fd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Controllare la timeline di riproduzione {#inspect-the-playback-timeline}

È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l&#39;applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell&#39;annuncio.

Di seguito è riportato un esempio di implementazione come mostrato nella schermata seguente.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Accedere all&#39; `Timeline` &#39;oggetto nel `MediaPlayer` metodo utilizzando il `getTimeline()` .

   La `Timeline` classe racchiude le informazioni correlate al contenuto della cronologia associata all&#39;elemento multimediale attualmente caricato dall&#39; `MediaPlayer` istanza. La `Timeline` classe fornisce l&#39;accesso a una vista di sola lettura della timeline sottostante. La `Timeline` classe fornisce un metodo getter che fornisce un iteratore attraverso un elenco di `TimelineMarker` oggetti.

1. Scorri l’elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

       Un oggetto `TimelineMarker` contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

1. Ascoltare l’ `MediaPlayerEvent.TIMELINE_UPDATED` evento sull’ `MediaPlayer` istanza e implementare il `TimelineUpdatedEventListener.onTimelineUpdated()` callback.

   L&#39; `Timeline` oggetto può informare l&#39;applicazione delle modifiche che potrebbero verificarsi nella timeline di riproduzione chiamando il `OnTimelineUpdated` listener.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
