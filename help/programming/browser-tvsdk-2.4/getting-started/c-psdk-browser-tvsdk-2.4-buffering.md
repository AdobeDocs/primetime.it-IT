---
description: Potete configurare gli elementi visivi per notificare all’utente il buffering del contenuto.
seo-description: Potete configurare gli elementi visivi per notificare all’utente il buffering del contenuto.
seo-title: Buffering
title: Buffering
uuid: da9498ee-c736-4093-97a2-250d3ad56d49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Buffering{#buffering}

Potete configurare gli elementi visivi per notificare all’utente il buffering del contenuto.

Ascoltare `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` ed `AdobePSDK.PSDKEventType.BUFFERING_END` eventi. Ad esempio:

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

Il framework dell&#39;interfaccia utente fornisce l&#39;implementazione predefinita del comportamento di buffering sovrapposto, che può essere esteso come illustrato di seguito:

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 
```

Esempio di DOM risultato:

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```

