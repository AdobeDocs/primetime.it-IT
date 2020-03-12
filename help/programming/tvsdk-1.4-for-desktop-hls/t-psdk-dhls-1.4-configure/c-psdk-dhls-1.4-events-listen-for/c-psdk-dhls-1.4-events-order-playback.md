---
description: TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-description: TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-title: Ordine degli eventi di riproduzione
title: Ordine degli eventi di riproduzione
uuid: 4a9ea66b-a383-46ff-9ab8-983b1dd7f935
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ordine degli eventi di riproduzione{#order-of-playback-events}

TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

Gli esempi seguenti mostrano l&#39;ordine di alcuni eventi che includono eventi di riproduzione.

* Quando si carica correttamente una risorsa multimediale tramite `MediaPlayer.replaceCurrentResource`, l&#39;ordine degli eventi è:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.INITIALIZED`

* Durante la preparazione per la riproduzione tramite `MediaPlayer.prepareToPlay`, l&#39;ordine degli eventi è:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` se sono stati inseriti degli annunci
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato `MediaPlayerStatus.PREPARED`

* Per i flussi live/lineari, durante la riproduzione con l&#39;avanzare della finestra di riproduzione e la risoluzione di ulteriori opportunità, l&#39;ordine degli eventi è:

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` se sono stati inseriti degli annunci

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

L&#39;esempio seguente mostra una progressione tipica degli eventi:

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

