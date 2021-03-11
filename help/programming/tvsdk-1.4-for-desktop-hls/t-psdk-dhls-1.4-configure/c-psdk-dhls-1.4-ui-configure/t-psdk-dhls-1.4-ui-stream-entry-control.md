---
description: Per impostazione predefinita, quando si avvia la riproduzione, il contenuto multimediale VOD inizia a 0 e il contenuto multimediale in tempo reale inizia dal punto live del client (DefaultMediaPlayer.LIVE_POINT).
title: Immettere un flusso in un momento specifico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Immettere un flusso in un momento specifico{#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, quando si avvia la riproduzione, il contenuto multimediale VOD inizia a 0 e il contenuto multimediale in tempo reale inizia dal punto live del client (DefaultMediaPlayer.LIVE_POINT).

Passa una posizione a `MediaPlayer.prepareToPlay`.

TVSDK considera la posizione specificata come punto iniziale della risorsa. Non è richiesta alcuna operazione di ricerca. Se la posizione non si trova all’interno dell’intervallo ricercabile, utilizza la posizione predefinita.

Ad esempio:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
