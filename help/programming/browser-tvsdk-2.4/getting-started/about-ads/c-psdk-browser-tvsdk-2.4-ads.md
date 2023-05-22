---
description: Durante la riproduzione del contenuto, il browser TVSDK può visualizzare annunci e trasmettere informazioni sugli annunci durante la creazione dell’oggetto MediaResource.
title: Annunci
exl-id: a44ad0fa-841f-474b-89f4-39666190231f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Panoramica {#ads-overview}

Durante la riproduzione del contenuto, il browser TVSDK può visualizzare annunci e trasmettere informazioni sugli annunci durante la creazione dell’oggetto MediaResource.

Facoltativamente, puoi chiamare il `prepareToPlay` dopo aver ricevuto `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

```js
function onStatusChange (event) { 
   switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
        player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
        break; 
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
        player.play(); 
        break; 
   } 
} 
 
var auditudeSettings     = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.domain  = "sample_auditude_domain"; 
auditudeSettings.mediaId = "sample_media_id"; 
auditudeSettings.zoneId  = "sample_zone_id"; 
 
// event handler 
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
 
var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
```

Browser TVSDK fornisce anche i seguenti eventi specifici per gli annunci che è possibile utilizzare nei gestori eventi per impedire l’inoltro rapido del contenuto durante la riproduzione degli annunci:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Per vedere come funziona nel framework dell’interfaccia utente, specifica le impostazioni annuncio nella configurazione come segue:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource: { 
 
            resourceUrl:'Specify Resource Url', 
 
            auditudeSettings: { 
                validMimeTypes: ["application/x-mpeURL"], 
                domain: "Sample_auditude_domain", 
                mediaId:"sample_media_id", 
                zoneID:"sample_zone_id", 
                creativeRepackagingEnabled:true 
            } 
        } 
    } 
}; 
```

Per ulteriori informazioni sulle `AuditudeSettings`, vedi [Metadati di inserimento annuncio](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).
