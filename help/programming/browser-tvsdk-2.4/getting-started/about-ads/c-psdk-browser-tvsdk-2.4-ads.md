---
description: Durante la riproduzione del contenuto, Browser TVSDK può visualizzare annunci e trasmettere informazioni sugli annunci durante la creazione dell'oggetto MediaResource.
seo-description: Durante la riproduzione del contenuto, Browser TVSDK può visualizzare annunci e trasmettere informazioni sugli annunci durante la creazione dell'oggetto MediaResource.
seo-title: Annunci
title: Annunci
uuid: 9a5e8c83-18ce-41e8-9cb1-fdc9da903faf
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Panoramica {#ads-overview}

Durante la riproduzione del contenuto, Browser TVSDK può visualizzare annunci e trasmettere informazioni sugli annunci durante la creazione dell&#39;oggetto MediaResource.

È possibile chiamare la funzione `prepareToPlay` dopo aver ricevuto `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

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

Browser TVSDK fornisce inoltre i seguenti eventi ad-specific che potete utilizzare nei gestori degli eventi per impedire che il contenuto venga inoltrato rapidamente durante la riproduzione degli annunci:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Per visualizzare questo funzionamento nel framework dell&#39;interfaccia utente, specificate le impostazioni di annuncio nella configurazione come segue:

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

Per ulteriori informazioni sulla `AuditudeSettings` richiesta, vedere [Aggiungi metadati di inserimento](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).
