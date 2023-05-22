---
description: Per il contenuto live/lineare, il browser TVSDK sostituisce un blocco del contenuto del flusso principale con un’interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga invariata.
title: Risoluzione e inserimento di annunci live/lineari
exl-id: 5d5954c6-9d1c-4900-9813-d3248fd61911
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Risoluzione e inserimento di annunci live/lineari{#live-linear-ad-resolving-and-insertion}

Per il contenuto live/lineare, il browser TVSDK sostituisce un blocco del contenuto del flusso principale con un’interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga invariata.

Prima e durante la riproduzione, il browser TVSDK risolve gli annunci noti, sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata e, se necessario, ricalcola la timeline virtuale. Le posizioni delle interruzioni pubblicitarie sono specificate dai cue point definiti dal manifesto.

Il browser TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che si trova all’inizio del contenuto.

Il browser TVSDK accetta l’interruzione pubblicitaria anche se la durata è più lunga o più breve della durata di sostituzione del punto di cue. Per impostazione predefinita, il browser TVSDK supporta `#EXT-X-CUE` suggerisci come marcatore di annuncio valido durante la risoluzione e il posizionamento di annunci. Questo marcatore richiede il campo metadati `DURATION` in secondi e l’ID univoco del cue. Ad esempio:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puoi definire e sottoscrivere ulteriori suggerimenti (tag).

Dopo l&#39;avvio della riproduzione, il motore video aggiorna periodicamente il file manifesto. Il browser TVSDK risolve eventuali nuovi annunci e inserisce gli annunci quando si incontra un punto di cue nel flusso live o lineare definito nel manifesto. Dopo la risoluzione e l’inserimento degli annunci, il TVSDK del browser calcola nuovamente la timeline virtuale e invia una `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` evento.

>[!TIP]
>
>Per i flussi live, Browser TVSDK supporta solo annunci pre-roll e mid-roll MP4 e HLS.
