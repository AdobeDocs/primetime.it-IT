---
description: Per i contenuti live/lineari, il browser TVSDK sostituisce una parte del contenuto del flusso principale con un’interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
title: Risoluzione e inserimento di annunci in tempo reale/lineare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Risoluzione e inserimento di annunci in tempo reale/lineare{#live-linear-ad-resolving-and-insertion}

Per i contenuti live/lineari, il browser TVSDK sostituisce una parte del contenuto del flusso principale con un’interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.

Prima e durante la riproduzione, Browser TVSDK risolve gli annunci noti, sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata e, se necessario, ricalcola la timeline virtuale. Le posizioni delle interruzioni pubblicitarie sono specificate dai punti di cue definiti dal manifesto.

Il browser TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che si trova all’inizio del contenuto.

Browser TVSDK accetta l&#39;interruzione pubblicitaria anche se la durata è più lunga o inferiore alla durata di sostituzione del punto di cue. Per impostazione predefinita, il browser TVSDK supporta il cue `#EXT-X-CUE` come indicatore di annunci valido durante la risoluzione e il posizionamento degli annunci. Questo marcatore richiede il campo metadati `DURATION` in secondi e l’ID univoco del cue. Ad esempio:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Puoi definire e sottoscrivere ulteriori suggerimenti (tag).

Dopo l&#39;avvio della riproduzione, il motore video aggiorna periodicamente il file manifesto. Browser TVSDK risolve eventuali nuovi annunci e inserisce gli annunci quando viene rilevato un punto di cue nel flusso live o lineare definito nel manifesto. Una volta risolti e inseriti gli annunci, il browser TVSDK calcola nuovamente la timeline virtuale e invia un evento `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` .

>[!TIP]
>
>Per i flussi live, il browser TVSDK supporta solo annunci pre-roll e mid-roll MP4 e HLS.

