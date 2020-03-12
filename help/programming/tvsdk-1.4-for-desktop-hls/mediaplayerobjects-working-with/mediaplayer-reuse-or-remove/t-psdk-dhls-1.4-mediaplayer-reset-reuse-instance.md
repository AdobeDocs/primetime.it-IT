---
description: Quando reimpostate un’istanza di MediaPlayer, viene riportato al relativo stato IDLE non inizializzato, come definito in MediaPlayerStatus.
seo-description: Quando reimpostate un’istanza di MediaPlayer, viene riportato al relativo stato IDLE non inizializzato, come definito in MediaPlayerStatus.
seo-title: Reimpostare o riutilizzare un'istanza di MediaPlayer
title: Reimpostare o riutilizzare un'istanza di MediaPlayer
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97

---


# Reimpostare o riutilizzare un&#39;istanza di MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

È possibile ripristinare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

Quando reimpostate un’istanza di MediaPlayer, viene riportato al relativo stato IDLE non inizializzato, come definito in MediaPlayerStatus.

Questa operazione è utile nei casi seguenti:

* Per riutilizzare un’ `MediaPlayer` istanza occorre caricarne una nuova `MediaResource` (contenuto video) e sostituire l’istanza precedente.

   La reimpostazione consente di riutilizzare l’ `MediaPlayer` istanza senza sovraccaricare le risorse, ricreare l’istanza `MediaPlayer`e riallocare le risorse. I metodi `replaceCurrentItem` e `replaceCurrentResource` i metodi eseguono automaticamente questi passaggi, senza dover chiamare il metodo reset.

* Quando `MediaPlayer` ha uno stato di ERRORE e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato di ERRORE.

1. Chiamata `reset` per restituire l’ `MediaPlayer` istanza allo stato non inizializzato:

   ```
   function reset():void; 
   ```

1. Utilizzate `MediaPlayer.replaceCurrentItem` o `MediaPlayer.replaceCurrentResource` per caricare un altro `MediaResource`.

   >[!TIP]
   >
   >Per cancellare un errore, caricate lo stesso `MediaResource`.

1. Quando ricevete il messaggio `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con lo `PREPARED` stato, avviate la riproduzione.
