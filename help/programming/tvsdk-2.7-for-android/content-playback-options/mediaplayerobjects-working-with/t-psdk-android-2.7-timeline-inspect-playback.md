---
description: Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo barra di scorrimento personalizzato in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.
title: Inspect la timeline di riproduzione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect la timeline di riproduzione {#inspect-the-playback-timeline}

Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo barra di scorrimento personalizzato in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.

Di seguito è riportato un esempio di implementazione, come mostrato nella schermata seguente.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Accedere a `Timeline` oggetto in `MediaPlayer` utilizzando `getTimeline()` metodo.

   Il `Timeline` La classe incapsula le informazioni correlate al contenuto della timeline associata all&#39;elemento multimediale attualmente caricato da `MediaPlayer` dell&#39;istanza. Il `Timeline` La classe consente di accedere a una visualizzazione di sola lettura della timeline sottostante. Il `Timeline` classe fornisce un metodo getter che fornisce un iteratore attraverso un elenco di `TimelineMarker` oggetti.

1. Scorrere l&#39;elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

       Un oggetto &quot;TimelineMarker&quot; contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

1. Ascolta la `MediaPlayerEvent.TIMELINE_UPDATED` evento sul `MediaPlayer` e implementare `TimelineUpdatedEventListener.onTimelineUpdated()` callback.

   Il `Timeline` può informare l’applicazione sulle modifiche che potrebbero verificarsi nella timeline di riproduzione chiamando il `OnTimelineUpdated` listener.

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
