---
description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-title: ' Inspect la timeline di riproduzione'
title: ' Inspect la timeline di riproduzione'
uuid: d0fe7926-9b9a-4203-a1c7-e57ba25b882e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


#  Inspect la timeline di riproduzione {#inspect-the-playback-timeline}

È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l&#39;applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell&#39;annuncio.

Di seguito è riportato un esempio di implementazione come mostrato nella schermata seguente.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Accedere all&#39;oggetto `Timeline` in `MediaPlayer` utilizzando il metodo `getTimeline()`.

   La classe `Timeline` racchiude le informazioni correlate al contenuto della cronologia associata all&#39;elemento multimediale attualmente caricato dall&#39;istanza `MediaPlayer`. La classe `Timeline` consente di accedere a una vista di sola lettura della timeline sottostante. La classe `Timeline` fornisce un metodo getter che fornisce un iteratore attraverso un elenco di oggetti `TimelineMarker`.

1. Iterate l&#39;elenco di `TimelineMarkers` e utilizzate le informazioni restituite per implementare la timeline.

       Un oggetto `TimelineMarker` contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

1. Ascoltare l&#39;evento `MediaPlayerEvent.TIMELINE_UPDATED` sull&#39;istanza `MediaPlayer` e implementare il callback `TimelineUpdatedEventListener.onTimelineUpdated()`.

   L&#39;oggetto `Timeline` può informare l&#39;applicazione delle modifiche che potrebbero verificarsi nella timeline di riproduzione chiamando il `OnTimelineUpdated` listener.

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
