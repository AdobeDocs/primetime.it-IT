---
description: Per il contenuto live/lineare, TVSDK sostituisce un blocco del contenuto del flusso principale con un’interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga invariata.
title: Risoluzione e inserimento di annunci live/lineari
exl-id: 2fe55c07-54d2-4a8a-a4e1-9e5ccae17ff9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Risoluzione e inserimento di annunci live/lineari {#resolve-and-insert-live-linear-ad}

Per il contenuto live/lineare, TVSDK sostituisce un blocco del contenuto del flusso principale con un’interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga invariata.

Prima e durante la riproduzione, TVSDK risolve gli annunci noti, sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata e, se necessario, ricalcola la timeline virtuale. Le posizioni delle interruzioni pubblicitarie sono specificate dai cue point definiti dal manifesto.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che viene inserito prima del contenuto.
* **Mid-roll**, che viene posizionato al centro del contenuto.

TVSDK accetta l’interruzione pubblicitaria anche se la durata è più lunga o più breve della durata di sostituzione del punto di cue. Per impostazione predefinita, TVSDK supporta `#EXT-X-CUE` suggerisci come marcatore di annuncio valido durante la risoluzione e il posizionamento di annunci. Questo marcatore richiede il campo metadati `DURATION` valore da esprimere in secondi e ID univoco del cue. Ad esempio:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puoi definire e sottoscrivere ulteriori suggerimenti (tag).

Dopo l&#39;avvio della riproduzione, il motore video aggiorna periodicamente il file manifesto. TVSDK risolve eventuali nuovi annunci e inserisce gli annunci quando si incontra un punto di cue nel flusso live o lineare definito nel manifesto. Dopo la risoluzione e l’inserimento degli annunci, TVSDK calcola nuovamente la timeline virtuale e invia una `TimelineItemsUpdatedEventListener.onTimelineUpdated` evento.
