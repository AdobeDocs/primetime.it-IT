---
description: Per i contenuti live/lineari, Browser TVSDK sostituisce una parte del contenuto del flusso principale con un'interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
seo-description: Per i contenuti live/lineari, Browser TVSDK sostituisce una parte del contenuto del flusso principale con un'interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
seo-title: Risoluzione e inserimento di annunci live/lineari
title: Risoluzione e inserimento di annunci live/lineari
uuid: 18c6733a-e827-4b1c-9cd5-796d57cbdb05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Risoluzione e inserimento di annunci live/lineari{#live-linear-ad-resolving-and-insertion}

Per i contenuti live/lineari, Browser TVSDK sostituisce una parte del contenuto del flusso principale con un&#39;interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.

Prima e durante la riproduzione, Browser TVSDK risolve gli annunci noti, sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata e, se necessario, ricalcola la timeline virtuale. Le posizioni delle interruzioni pubblicitarie sono specificate dai cue point definiti dal manifest.

Il browser TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che si trova all&#39;inizio del contenuto.

Browser TVSDK accetta l&#39;interruzione dell&#39;annuncio anche se la durata è maggiore o inferiore alla durata di sostituzione del cue point. Per impostazione predefinita, Browser TVSDK supporta il `#EXT-X-CUE` cue point come indicatore pubblicitario valido per la risoluzione e il posizionamento degli annunci. Questo marcatore richiede il campo di metadati `DURATION` in secondi e l&#39;ID univoco del cue point. Ad esempio:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puoi definire e iscriverti ad altri suggerimenti (tag).

Dopo l’avvio della riproduzione, il motore video aggiorna periodicamente il file manifesto. Browser TVSDK risolve eventuali nuovi annunci e inserisce gli annunci quando viene rilevato un cue point nel flusso live o lineare definito nel manifesto. Una volta risolti e inseriti gli annunci, Browser TVSDK calcola di nuovo la timeline virtuale e invia un `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` evento.

>[!TIP]
>
>Per i flussi live, l&#39;SDK per browser TVSDK supporta solo annunci pre-roll e mid-roll MP4 e HLS.

