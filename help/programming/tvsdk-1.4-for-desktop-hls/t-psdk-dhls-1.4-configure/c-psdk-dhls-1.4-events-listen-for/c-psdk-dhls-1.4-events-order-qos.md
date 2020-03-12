---
description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e di ricerca.
seo-description: TVSDK invia eventi di qualità del servizio (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e di ricerca.
seo-title: Eventi QoS
title: Eventi QoS
uuid: e6ba1e9b-435b-480d-bea9-bff41b4e0b21
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Eventi QoS{#qos-events}

TVSDK invia eventi di qualità del servizio (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche di QoS, ad esempio eventi di buffering e di ricerca.

L&#39;esempio seguente mostra una tipica progressione di questi eventi:

```
// For buffering 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_BEGIN, onBufferingBegin); 
private function onBufferingBegin(event:BufferEvent):void { ... } 
 
mediaPlayer.addEventListener(BufferEvent.BUFFERING_END, onBufferingCompleted); 
private function onBufferingCompleted(event:BufferEvent):void { ... } 
 
// For seeking 
mediaPlayer.addEventListener(SeekEvent.SEEK_BEGIN, onSeekBegin); 
private function onSeekBegin(event:SeekEvent):void { ... } 
 
mediaPlayer.addEventListener(SeekEvent.SEEK_COMPLETED, onSeekCompleted); 
private function onSeekCompleted(event:SeekEvent):void { ... } 
 
...  SeekEvent.SEEK_POSITION_ADJUSTED...  //if the desired 
// seek position is modified by the current advertising policies 
```

