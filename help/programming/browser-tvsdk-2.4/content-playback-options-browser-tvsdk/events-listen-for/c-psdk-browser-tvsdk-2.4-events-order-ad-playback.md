---
description: Quando la riproduzione include la pubblicità, il browser TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni in base agli eventi nella sequenza prevista.
title: Ordine degli eventi pubblicitari
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Ordine degli eventi pubblicitari{#order-of-advertising-events}

Quando la riproduzione include la pubblicità, il browser TVSDK invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni in base agli eventi nella sequenza prevista.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Durante la riproduzione degli annunci, l&#39;ordine degli eventi è:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* I seguenti vengono inviati per ogni annuncio nell’interruzione pubblicitaria:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (più volte durante la riproduzione di un annuncio)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

L’esempio seguente mostra una progressione tipica degli eventi di riproduzione di annunci:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

