---
description: Il browser TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-description: Il browser TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-title: Ordine degli eventi di riproduzione
title: Ordine degli eventi di riproduzione
uuid: 259a9a2d-3d28-4240-b392-cc81f5c3f0cf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ordine degli eventi di riproduzione{#order-of-playback-events}

Il browser TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

Gli esempi seguenti mostrano l&#39;ordine di alcuni eventi che includono eventi di riproduzione.

* Quando si carica correttamente una risorsa multimediale tramite `replaceCurrentResource`, l&#39;ordine degli eventi è:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* Durante la preparazione per la riproduzione tramite `MediaPlayer.prepareToPlay`, l&#39;ordine degli eventi è:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

L&#39;esempio seguente mostra una progressione tipica degli eventi:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```

