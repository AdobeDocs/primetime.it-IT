---
description: TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni in base agli eventi nella sequenza prevista.
title: Ordine degli eventi di riproduzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Ordine degli eventi di riproduzione{#order-of-playback-events}

TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni in base agli eventi nella sequenza prevista.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

Gli esempi seguenti mostrano l’ordine di alcuni eventi che includono eventi di riproduzione.

* Quando si carica correttamente una risorsa multimediale tramite `MediaPlayer.replaceCurrentResource`, l&#39;ordine degli eventi è:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato  `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato  `MediaPlayerStatus.INITIALIZED`

* Durante la preparazione della riproduzione tramite `MediaPlayer.prepareToPlay`, l&#39;ordine degli eventi è:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato  `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` se sono stati inseriti annunci
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato  `MediaPlayerStatus.PREPARED`

* Per i flussi in tempo reale/lineare, durante la riproduzione con l&#39;avanzamento della finestra di riproduzione e la risoluzione di ulteriori opportunità, l&#39;ordine degli eventi è:

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` se sono stati inseriti annunci

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

L’esempio seguente mostra una progressione tipica degli eventi:

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```

