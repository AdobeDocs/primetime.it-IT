---
description: Quando la riproduzione include la pubblicità, Browser TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-description: Quando la riproduzione include la pubblicità, Browser TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.
seo-title: Ordine degli eventi pubblicitari
title: Ordine degli eventi pubblicitari
uuid: 9787e6ac-5e52-4d7d-8fc7-f7609633707c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ordine degli eventi pubblicitari{#order-of-advertising-events}

Quando la riproduzione include la pubblicità, Browser TVSDK invia eventi/notifiche nelle sequenze generalmente previste. Il lettore può implementare azioni basate su eventi nella sequenza prevista.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Durante la riproduzione di annunci, l&#39;ordine degli eventi è:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* Le azioni seguenti vengono inviate per ogni annuncio nell&#39;interruzione di annuncio:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (più volte durante la riproduzione di un annuncio)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

L&#39;esempio seguente mostra una progressione tipica degli eventi di riproduzione di annunci:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

