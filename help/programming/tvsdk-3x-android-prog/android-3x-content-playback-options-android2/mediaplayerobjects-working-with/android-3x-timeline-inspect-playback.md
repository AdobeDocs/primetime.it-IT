---
description: Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.
title: Inspect la timeline di riproduzione
exl-id: 95792354-76f6-44fd-9207-73e862b434e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect la timeline di riproduzione {#inspect-the-playback-timeline}

Puoi ottenere una descrizione della timeline associata all’elemento attualmente selezionato riprodotto da TVSDK. Questa funzione è particolarmente utile quando l’applicazione visualizza un controllo personalizzato a barre di scorrimento in cui vengono identificate le sezioni di contenuto corrispondenti al contenuto dell’annuncio.

Ecco un esempio di implementazione, come mostrato nella schermata successiva.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Accedere al `Timeline` nell&#39;oggetto `MediaPlayer` utilizzando `getTimeline()` metodo .

   La `Timeline` incapsula le informazioni correlate al contenuto della timeline associata all&#39;elemento multimediale attualmente caricato dal `MediaPlayer` istanza. La `Timeline` La classe fornisce l&#39;accesso a una visualizzazione in sola lettura della timeline sottostante. La `Timeline` Classe fornisce un metodo getter che fornisce un iteratore attraverso un elenco `TimelineMarker` oggetti.

1. Itera attraverso l&#39;elenco di `TimelineMarkers` e utilizza le informazioni restituite per implementare la timeline.

       Un oggetto `TimelineMarker` contiene due informazioni:
   
   * Posizione del marcatore sulla timeline (in millisecondi)
   * Durata del marcatore sulla timeline (in millisecondi)

1. Ascolta i `MediaPlayerEvent.TIMELINE_UPDATED` sull&#39;evento `MediaPlayer` e implementa `TimelineUpdatedEventListener.onTimelineUpdated()` callback.

   La `Timeline` L&#39;oggetto può informare l&#39;applicazione delle modifiche che potrebbero verificarsi nella timeline della riproduzione chiamando il `OnTimelineUpdated` ascoltatore.

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
