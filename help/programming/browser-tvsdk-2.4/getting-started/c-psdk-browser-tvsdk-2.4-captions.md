---
description: Potete visualizzare le didascalie durante la riproduzione del contenuto video.
seo-description: Potete visualizzare le didascalie durante la riproduzione del contenuto video.
seo-title: Sottotitoli
title: Sottotitoli
uuid: 4dedcedc-50e5-4983-bb09-3f316337117e
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 3%

---


# Sottotitoli{#captions}

Potete visualizzare le didascalie durante la riproduzione del contenuto video.

Per gestire le didascalie, è necessario aggiungere il listener di `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` eventi:

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

Il framework dell&#39;interfaccia utente fornisce un&#39;implementazione predefinita dei comportamenti per le didascalie, che può essere modificata. I comportamenti dei sottotitoli codificati possono essere modificati anche estendendo i comportamenti predefiniti dei sottotitoli codificati. Ad esempio:

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
