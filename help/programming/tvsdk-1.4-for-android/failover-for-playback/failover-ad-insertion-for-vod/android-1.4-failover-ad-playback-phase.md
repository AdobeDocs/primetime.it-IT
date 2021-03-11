---
description: TVSDK scarica i segmenti di annunci ed effettua il rendering sullo schermo del dispositivo.
title: Fase di riproduzione annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Fase di riproduzione annunci{#ad-playback-phase}

TVSDK scarica i segmenti di annunci ed effettua il rendering sullo schermo del dispositivo.

A questo punto, TVSDK ha risolto gli annunci, li ha posizionati sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

In questa fase potrebbero verificarsi le seguenti principali classi di errori:

* Errori durante la connessione al server host
* Errori durante il download del file manifesto
* Errori durante il download dei segmenti multimediali

Per tutte e tre le classi di errore, TVSDK inoltra gli eventi attivati all&#39;applicazione, tra cui:

* Eventi di notifica attivati quando si verifica un failover.
* Eventi di notifica quando il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Eventi di notifica attivati quando sono state prese in considerazione tutte le opzioni di failover e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

   La tua applicazione deve intraprendere l&#39;azione appropriata.

Che si verifichino o meno errori, TVSDK chiama AdBreakComplete per ogni `onAdBreakStart` e `onAdComplete` per ogni `onAdStart`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero esserci spazi nella timeline. Quando gli spazi vuoti sono sufficientemente grandi, i valori nella posizione della testina di riproduzione e l&#39;avanzamento dell&#39;annuncio riportato potrebbero presentare delle discontinuità.
