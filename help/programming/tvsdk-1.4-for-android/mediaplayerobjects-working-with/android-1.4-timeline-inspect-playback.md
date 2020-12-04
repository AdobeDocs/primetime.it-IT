---
description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-description: È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l'applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell'annuncio.
seo-title: ' Inspect la timeline di riproduzione'
title: ' Inspect la timeline di riproduzione'
uuid: b5ede131-1037-449b-bc3f-a066fdc92fc5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


#  Inspect la timeline di riproduzione{#inspect-the-playback-timeline}

È possibile ottenere una descrizione della cronologia associata all’elemento attualmente selezionato riprodotto da TVSDK. Ciò è particolarmente utile quando l&#39;applicazione visualizza un controllo personalizzato della barra di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell&#39;annuncio.

Di seguito è riportato un esempio di implementazione come mostrato nella schermata seguente.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Accedere all&#39;oggetto `Timeline` in `MediaPlayer` utilizzando il metodo `getTimeline`.

   La classe `Timeline` racchiude le informazioni correlate al contenuto della cronologia associata all&#39;elemento multimediale attualmente caricato dall&#39;istanza `MediaPlayer`. La classe `Timeline` consente di accedere a una vista di sola lettura della timeline sottostante. La classe `Timeline` fornisce un metodo getter che fornisce un iteratore attraverso un elenco di oggetti `TimelineMarker`.

1. Iterate l&#39;elenco di `TimelineMarkers` e utilizzate le informazioni restituite per implementare la timeline.

       Un oggetto `TimelineMarker` contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

1. Implementare l&#39;interfaccia di callback del listener `MediaPlayer.PlaybackEventListener.onTimelineUpdated` e registrarla con l&#39;oggetto `Timeline`.

   L&#39;oggetto `Timeline` può informare l&#39;applicazione delle modifiche che potrebbero verificarsi nella timeline di riproduzione chiamando il `OnTimelineUpdated` listener.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```

