---
description: TVSDK invia eventi Quality of Service (QoS) per notificare all'applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come ad esempio gli eventi di buffering e ricerca.
title: Eventi QoS
exl-id: 283555cd-9ba9-45e9-a73e-76aba6993e8a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 0%

---

# Eventi QoS{#qos-events}

TVSDK invia eventi Quality of Service (QoS) per notificare all&#39;applicazione gli eventi che potrebbero influenzare il calcolo delle statistiche QoS, come ad esempio gli eventi di buffering e ricerca.

L’esempio seguente mostra una progressione tipica di questi eventi:

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
