---
description: Quando la riproduzione include la pubblicità, TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-description: Quando la riproduzione include la pubblicità, TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-title: Ordine degli eventi pubblicitari
title: Ordine degli eventi pubblicitari
uuid: 34a6a606-2f2e-42de-88fd-c91202cafddf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Ordine degli eventi pubblicitari{#order-of-advertising-events}

Quando la riproduzione include la pubblicità, TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Durante la riproduzione di annunci, l&#39;ordine degli eventi è:

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* Le azioni seguenti vengono inviate per ogni annuncio nell&#39;interruzione di annuncio:

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` (più volte durante la riproduzione di un annuncio)
   * `AdClickEvent.AD_CLICK` (per ogni clic)
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

L&#39;esempio seguente mostra una progressione tipica degli eventi di riproduzione di annunci:

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 
```

