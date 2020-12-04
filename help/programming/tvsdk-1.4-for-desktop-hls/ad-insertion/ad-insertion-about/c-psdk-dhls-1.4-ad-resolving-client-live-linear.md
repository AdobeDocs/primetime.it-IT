---
description: Per i contenuti live/lineari, TVSDK sostituisce una parte del contenuto del flusso principale con un'interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
seo-description: Per i contenuti live/lineari, TVSDK sostituisce una parte del contenuto del flusso principale con un'interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.
seo-title: Risoluzione e inserimento di annunci live/lineari
title: Risoluzione e inserimento di annunci live/lineari
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Risoluzione e inserimento di annunci live/lineari{#live-linear-ad-resolving-and-insertion}

Per i contenuti live/lineari, TVSDK sostituisce una parte del contenuto del flusso principale con un&#39;interruzione pubblicitaria della stessa durata, in modo che la durata della timeline rimanga la stessa.

Prima e durante la riproduzione, TVSDK risolve gli annunci noti, sostituisce parti del contenuto principale con interruzioni pubblicitarie della stessa durata e, se necessario, ricalcola la timeline virtuale. Le posizioni delle interruzioni pubblicitarie sono specificate dai cue point definiti dal manifest.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che si trova all&#39;inizio del contenuto.
* **Media roll**, che si trova al centro del contenuto.

TVSDK accetta l&#39;interruzione dell&#39;annuncio anche se la durata è più lunga o più breve della durata di sostituzione del cue point. Per impostazione predefinita, TVSDK supporta il cue `#EXT-X-CUE` come indicatore pubblicitario valido per la risoluzione e il posizionamento degli annunci. Questo marcatore richiede il campo di metadati `DURATION` in secondi e l&#39;ID univoco del cue point. Ad esempio:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>Durante l&#39;implementazione di un `AdPolicySelector` consueto, è possibile definire un criterio diverso per il pre-roll, il mid-roll e il post-roll `AdBreakTimelineItem`s in `AdPolicyInfo`, che si basa sul tipo di `AdBreakTimelineItem`s. Ad esempio, potete mantenere il contenuto mid-roll dopo che è stato riprodotto ma rimuovere il contenuto pre-roll dopo che è stato riprodotto.

Dopo l’avvio della riproduzione, il motore video aggiorna periodicamente il file manifesto. TVSDK risolve eventuali nuovi annunci e inserisce gli annunci quando viene rilevato un cue point nel flusso live o lineare definito nel manifesto. Dopo che gli annunci sono stati risolti e inseriti, TVSDK calcola di nuovo la timeline virtuale e invia un evento `TimelineEvent.TIMELINE_UPDATED`.
