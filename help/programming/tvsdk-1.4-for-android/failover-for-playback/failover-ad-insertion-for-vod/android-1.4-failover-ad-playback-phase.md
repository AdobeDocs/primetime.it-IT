---
description: TVSDK scarica i segmenti di annunci e li visualizza sullo schermo del dispositivo.
seo-description: TVSDK scarica i segmenti di annunci e li visualizza sullo schermo del dispositivo.
seo-title: Fase ad-riproduzione
title: Fase ad-riproduzione
uuid: 1bbcea08-3475-4a64-9f89-c455d5dd828e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fase ad-riproduzione{#ad-playback-phase}

TVSDK scarica i segmenti di annunci e li visualizza sullo schermo del dispositivo.

A questo punto, TVSDK ha risolto gli annunci, li ha posizionati sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

In questa fase potrebbero verificarsi le seguenti classi principali di errori:

* Errori durante la connessione al server host
* Errori durante il download del file manifesto
* Errori durante il download dei segmenti multimediali

Per tutte e tre le classi di errore, TVSDK inoltra all&#39;applicazione gli eventi attivati, inclusi:

* Eventi di notifica attivati in caso di failover.
* Eventi di notifica quando il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Gli eventi di notifica attivati quando sono state prese in considerazione tutte le opzioni di failover e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

   La tua applicazione deve intraprendere l&#39;azione appropriata.

Che si verifichino o meno errori, TVSDK chiama adAdBreakComplete per ogni `onAdBreakStart` e `onAdComplete` per ogni `onAdStart`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero verificarsi degli spazi nella timeline. Quando gli spazi vuoti sono sufficientemente grandi, i valori nella posizione dell&#39;indicatore di riproduzione e l&#39;avanzamento degli annunci riportati potrebbero mostrare delle discontinuità.
