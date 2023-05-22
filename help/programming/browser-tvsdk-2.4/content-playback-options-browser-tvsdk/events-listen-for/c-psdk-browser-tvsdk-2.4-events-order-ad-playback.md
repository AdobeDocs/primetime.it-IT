---
description: Quando la riproduzione include annunci, il TVSDK del browser invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate sugli eventi nella sequenza prevista.
title: Ordine degli eventi pubblicitari
exl-id: fcc40aa8-9364-40a8-b2f2-9327e24819af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Ordine degli eventi pubblicitari{#order-of-advertising-events}

Quando la riproduzione include annunci, il TVSDK del browser invia eventi/notifiche in sequenze generalmente previste. Il lettore può implementare azioni basate sugli eventi nella sequenza prevista.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Durante la riproduzione degli annunci, l’ordine degli eventi è:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* I seguenti vengono inviati per ogni annuncio nell’interruzione pubblicitaria:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (più volte durante la riproduzione di un annuncio)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

L’esempio seguente mostra una progressione tipica degli eventi di riproduzione degli annunci:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
