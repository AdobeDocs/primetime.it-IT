---
description: Durante la riproduzione del contenuto, il browser TVSDK può visualizzare gli annunci e trasmettere informazioni sugli annunci durante la creazione dell'oggetto MediaResource.
title: Annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# Panoramica {#ads-overview}

Durante la riproduzione del contenuto, il browser TVSDK può visualizzare gli annunci e trasmettere informazioni sugli annunci durante la creazione dell&#39;oggetto MediaResource.

Facoltativamente, puoi chiamare la funzione `prepareToPlay` dopo aver ricevuto `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

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

Il browser TVSDK fornisce anche i seguenti eventi specifici per gli annunci che è possibile utilizzare nei gestori di eventi per impedire l’inoltro rapido dei contenuti durante la riproduzione degli annunci:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Per visualizzare questo funzionamento nel framework dell&#39;interfaccia utente, specifica le impostazioni degli annunci nella configurazione come segue:

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

Per ulteriori informazioni sul `AuditudeSettings` richiesto, consulta [Metadati di inserimento annunci](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).
