---
description: Per i contenuti live/lineari, TVSDK sostituisce una parte del contenuto del flusso principale con un'interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
seo-description: Per i contenuti live/lineari, TVSDK sostituisce una parte del contenuto del flusso principale con un'interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
seo-title: Risoluzione e inserimento di annunci live/lineari
title: Risoluzione e inserimento di annunci live/lineari
uuid: c9d54fc9-1d54-41c3-a872-d27afdd16314
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Risolvere e inserire annunci live/lineari {#resolve-and-insert-live-linear-ad}

Per i contenuti live/lineari, TVSDK sostituisce una parte del contenuto del flusso principale con un&#39;interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.

Prima e durante la riproduzione, TVSDK risolve gli annunci noti, sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata e, se necessario, ricalcola la timeline virtuale. Le posizioni delle interruzioni pubblicitarie sono specificate dai cue point definiti dal manifest.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che viene posizionato prima del contenuto.
* **Mid-roll**, che viene posizionato al centro del contenuto.

TVSDK accetta l&#39;interruzione dell&#39;annuncio anche se la durata è più lunga o più breve della durata di sostituzione del cue point. Per impostazione predefinita, TVSDK supporta il `#EXT-X-CUE` cue point come indicatore pubblicitario valido per la risoluzione e il posizionamento degli annunci. Questo marcatore richiede che il valore del campo di metadati `DURATION` sia espresso in secondi e l&#39;ID univoco del cue point. Ad esempio:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puoi definire e iscriverti ad altri suggerimenti (tag).

Dopo l’avvio della riproduzione, il motore video aggiorna periodicamente il file manifesto. TVSDK risolve eventuali nuovi annunci e inserisce gli annunci quando viene rilevato un cue point nel flusso live o lineare definito nel manifesto. Dopo che gli annunci sono stati risolti e inseriti, TVSDK calcola di nuovo la timeline virtuale e invia un `TimelineItemsUpdatedEventListener.onTimelineUpdated` evento.
