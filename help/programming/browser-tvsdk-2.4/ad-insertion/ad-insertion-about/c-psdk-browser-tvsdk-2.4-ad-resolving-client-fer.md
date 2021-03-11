---
description: 'Il contenuto Full Event Replay (FER) è un flusso live convertito in VOD aggiungendo il tag #EXT-X-ENDLIST alla fine del file manifesto. Il flusso mantiene i marcatori di cue degli annunci.'
title: Risoluzione e inserimento di annunci gratuiti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Risoluzione e inserimento di annunci FER{#fer-ad-resolving-and-insertion}

Il contenuto Full Event Replay (FER) è un flusso live convertito in VOD aggiungendo il tag #EXT-X-ENDLIST alla fine del file manifesto. Il flusso mantiene i marcatori di cue degli annunci.

Il browser TVSDK tratta un flusso FER come VOD, quindi per impostazione predefinita la modalità di segnalazione degli annunci è `SERVER_MAP`. Tuttavia, poiché il flusso mantiene i suoi marcatori di cue degli annunci, puoi impostare la modalità di segnalazione degli annunci su `MANIFEST_CUES`, che consente di utilizzare i marcatori di cue degli annunci per l’inserimento degli annunci.

Per attivare l&#39;inserimento di annunci utilizzando i marcatori cue per un flusso FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

Il comportamento di risoluzione e inserimento di annunci gratuiti è simile alla risoluzione e all&#39;inserimento di annunci live. Il browser TVSDK effettua le seguenti operazioni:

1. Inserisce eventuali annunci pre-scorrimento all’inizio del contenuto.
1. Risolve gli annunci specificati dai punti di cue definiti nel manifesto.
1. Sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata
1. Se necessario, ricalcola la timeline virtuale.

**Restrizione:** il browser TVSDK supporta solo la riproduzione di flussi HLS FER. Inoltre, gli annunci MP4 mid-roll non sono supportati con flussi FER.
