---
description: 'Il contenuto Full Event Replay (FER) è un flusso live convertito in VOD aggiungendo il tag #EXT-X-ENDLIST alla fine del file manifesto. Il flusso mantiene i relativi marcatori di cue annuncio.'
seo-description: 'Il contenuto Full Event Replay (FER) è un flusso live convertito in VOD aggiungendo il tag #EXT-X-ENDLIST alla fine del file manifesto. Il flusso mantiene i relativi marcatori di cue annuncio.'
seo-title: Risoluzione e inserimento di annunci gratuiti
title: Risoluzione e inserimento di annunci gratuiti
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Risoluzione e inserimento annunci FER{#fer-ad-resolving-and-insertion}

Il contenuto Full Event Replay (FER) è un flusso live convertito in VOD aggiungendo il tag #EXT-X-ENDLIST alla fine del file manifesto. Il flusso mantiene i relativi marcatori di cue annuncio.

Browser TVSDK tratta un flusso FER come VOD, quindi per impostazione predefinita la modalità di segnalazione degli annunci è `SERVER_MAP`. Tuttavia, poiché il flusso mantiene i marcatori di cue annunci, potete impostare la modalità di segnalazione annunci su `MANIFEST_CUES`, che consente di utilizzare i marcatori di cue per gli annunci per l&#39;inserimento degli annunci.

Per attivare l’inserimento di annunci utilizzando i marcatori di cue per un flusso FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

Il comportamento di risoluzione e inserimento di annunci gratuiti è simile alla risoluzione e all&#39;inserimento live degli annunci. Il browser TVSDK effettua le seguenti operazioni:

1. Inserisce eventuali annunci pre-roll all&#39;inizio del contenuto.
1. Risolve gli annunci specificati dai cue point definiti nel manifest.
1. Sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata
1. Se necessario, ricalcola la timeline virtuale.

**Limitazione:** Browser TVSDK supporta solo la riproduzione di flussi FER HLS. Inoltre, gli annunci mid-roll MP4 non sono supportati con flussi FER.
