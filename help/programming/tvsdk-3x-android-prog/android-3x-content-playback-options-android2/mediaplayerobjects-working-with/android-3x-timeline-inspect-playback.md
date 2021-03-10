---
description: Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.
title: Inspect la timeline di riproduzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Inspect la timeline di riproduzione {#inspect-the-playback-timeline}

Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.

Ecco un esempio di implementazione, come mostrato nella schermata successiva.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Accedi all&#39;oggetto `Timeline` in `MediaPlayer` utilizzando il metodo `getTimeline()` .

   La classe `Timeline` incapsula le informazioni correlate al contenuto della timeline associata all&#39;elemento multimediale attualmente caricato dall&#39;istanza `MediaPlayer`. La classe `Timeline` consente di accedere a una visualizzazione in sola lettura della timeline sottostante. La classe `Timeline` fornisce un metodo getter che fornisce un iteratore attraverso un elenco di oggetti `TimelineMarker`.

1. Itera l’elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

       Un oggetto `TimelineMarker` contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

1. Ascolta l’evento `MediaPlayerEvent.TIMELINE_UPDATED` sull’istanza `MediaPlayer` e implementa il callback `TimelineUpdatedEventListener.onTimelineUpdated()` .

   L&#39;oggetto `Timeline` può informare l&#39;applicazione delle modifiche che potrebbero verificarsi nella timeline di riproduzione chiamando il listener `OnTimelineUpdated`.

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
