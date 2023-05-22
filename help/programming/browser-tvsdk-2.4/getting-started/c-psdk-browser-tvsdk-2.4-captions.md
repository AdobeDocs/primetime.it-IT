---
description: È possibile visualizzare i sottotitoli durante la riproduzione di contenuti video.
title: Sottotitoli
exl-id: 2144a6b2-0b9a-49ea-ad44-997adf36cbe6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# Sottotitoli{#captions}

È possibile visualizzare i sottotitoli durante la riproduzione di contenuti video.

Per gestire i sottotitoli, devi aggiungere `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` listener di eventi:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.CAPTIONS_UPDATED,  
                        onCaptionsUpdateEvent); 
... 
function onCaptionsUpdateEvent (event) { 
  // code to show the captions icon and any settings button. 
<pre>
   For example: 
  var btnCC = document.getElementById("btn_captions"); 
   btnCC.classList.remove("invisible"); 
   
  var btnSettings = document.getElementById("btn_settings"); 
   btnSettings.classList.remove("invisible"); 
 } 
</pre>
```

Il framework dell’interfaccia utente fornisce un’implementazione dei comportamenti di didascalia predefinita, che può essere modificata. I comportamenti dei sottotitoli codificati possono essere modificati anche estendendo i comportamenti predefiniti dei sottotitoli codificati. Ad esempio:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer(‘.videoDiv', { 
player:{ 
    mediaResource: 'Specify Resource URL', 
    ccStyle: { 
    font:AdobePSDK.TextFormat.CURSIVE, 
    fontColor:AdobePSDK.TextFormat.BRIGHT_WHITE, 
    edgeColor:AdobePSDK.TextFormat.BLUE, 
    backgroundColor:AdobePSDK.TextFormat.BLACK, 
    fillColor:AdobePSDK.TextFormat.BLUE, 
    size:AdobePSDK.TextFormat.MEDIUM, 
    fontOpacity:100, 
    backgroundOpacity:1, 
    fillOpacity:1 
   } 
 } 
 
}); 
```
