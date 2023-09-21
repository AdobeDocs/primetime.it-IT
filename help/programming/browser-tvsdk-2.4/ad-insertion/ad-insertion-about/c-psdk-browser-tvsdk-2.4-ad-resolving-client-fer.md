---
description: Il contenuto FER (Full Event Replay) è un flusso live convertito in VOD aggiungendo il tag
title: Risoluzione e inserimento di annunci FER
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Risoluzione e inserimento di annunci FER{#fer-ad-resolving-and-insertion}

Il contenuto FER (Full Event Replay) è un flusso live convertito in VOD aggiungendo il tag #EXT-X-ENDLIST alla fine del file manifesto. Il flusso mantiene i marcatori di cue dell’annuncio.

Il browser TVSDK tratta un flusso FER come VOD, quindi per impostazione predefinita la modalità di segnalazione dell’annuncio è `SERVER_MAP`. Tuttavia, poiché il flusso mantiene i suoi marcatori di cue dell’annuncio, puoi impostare la modalità di segnalazione dell’annuncio su `MANIFEST_CUES`, che consente di utilizzare i marcatori di cue dell’annuncio per l’inserimento degli annunci.

Per attivare l’inserimento di annunci utilizzando marcatori cue per un flusso FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

Il comportamento di risoluzione e inserimento degli annunci FER è simile a quello di risoluzione e inserimento degli annunci live. TVSDK per browser esegue le seguenti operazioni:

1. Inserisce eventuali annunci pre-roll all’inizio del contenuto.
1. Risolve gli annunci specificati dai cue point definiti nel manifesto.
1. Sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata
1. Ricalcola la timeline virtuale, se necessario.

**Limitazione:** Browser TVSDK supporta solo la riproduzione di flussi HLS FER. Inoltre, gli annunci MP4 mid-roll non sono supportati con i flussi FER.
