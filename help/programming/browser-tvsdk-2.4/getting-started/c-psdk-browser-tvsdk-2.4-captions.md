---
description: È possibile visualizzare le didascalie durante la riproduzione di contenuto video.
title: Sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 3%

---


# Sottotitoli{#captions}

È possibile visualizzare le didascalie durante la riproduzione di contenuto video.

Per gestire le didascalie, è necessario aggiungere il listener di eventi `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED`:

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

Il framework dell&#39;interfaccia utente fornisce un&#39;implementazione predefinita dei comportamenti per le didascalie, che può essere modificata. I comportamenti dei sottotitoli codificati possono essere modificati anche estendendo i comportamenti predefiniti dei sottotitoli. Ad esempio:

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
