---
description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (DefaultMediaPlayer.LIVE_POINT).
seo-description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (DefaultMediaPlayer.LIVE_POINT).
seo-title: Inserire un flusso in un momento specifico
title: Inserire un flusso in un momento specifico
uuid: f58d908a-77b9-465f-b3a9-8fe63a249d39
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 1%

---


# Immettere un flusso in un momento specifico{#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (DefaultMediaPlayer.LIVE_POINT).

Passa una posizione a `MediaPlayer.prepareToPlay`.

TVSDK considera la posizione specificata come punto di partenza per la risorsa. Non è richiesta alcuna operazione di ricerca. Se la posizione non è all’interno dell’intervallo ricercabile, utilizza la posizione predefinita.

Ad esempio:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
