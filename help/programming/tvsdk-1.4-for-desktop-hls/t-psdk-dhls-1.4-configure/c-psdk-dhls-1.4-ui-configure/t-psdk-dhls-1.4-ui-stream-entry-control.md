---
description: Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 e il contenuto multimediale live inizia dal punto di attivazione del client (DefaultMediaPlayer.LIVE_POINT).
title: Immettere un flusso in un momento specifico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Immettere un flusso in un momento specifico{#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 e il contenuto multimediale live inizia dal punto di attivazione del client (DefaultMediaPlayer.LIVE_POINT).

Passa una posizione a `MediaPlayer.prepareToPlay`.

TVSDK considera la posizione specificata come punto di partenza della risorsa. Non è richiesta alcuna operazione di ricerca. Se la posizione non si trova all&#39;interno dell&#39;intervallo ricercabile, utilizza la posizione predefinita.

Ad esempio:

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
