---
description: TVSDK scarica i segmenti dell’annuncio ed esegue il rendering sullo schermo del dispositivo.
title: Fase riproduzione annuncio
exl-id: c12dcf84-0daa-4bc2-8e17-fdf47a760296
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Fase riproduzione annuncio{#ad-playback-phase}

TVSDK scarica i segmenti dell’annuncio ed esegue il rendering sullo schermo del dispositivo.

A questo punto, TVSDK ha risolto gli annunci, li ha posizionati sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

In questa fase possono verificarsi le seguenti classi principali di errori:

* Errori durante la connessione al server host
* Errori durante il download del file manifesto
* Errori durante il download dei segmenti multimediali

Per tutte e tre le classi di errore, TVSDK inoltra gli eventi attivati all’applicazione, tra cui:

* Eventi di notifica attivati quando si verifica un failover.
* Eventi di notifica quando il profilo viene modificato a causa dell’algoritmo di failover.
* Gli eventi di notifica vengono attivati quando tutte le opzioni di failover sono state considerate e non è possibile eseguire alcuna azione aggiuntiva automaticamente.

   L&#39;applicazione deve intraprendere l&#39;azione appropriata.

Che si verifichino o meno errori, TVSDK chiama onAdBreakComplete per ogni `onAdBreakStart` e `onAdComplete` per ogni `onAdStart`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero esserci degli spazi nella timeline. Quando gli spazi sono sufficientemente ampi, i valori nella posizione della testina di riproduzione e l’avanzamento dell’annuncio riportato potrebbero mostrare discontinuità.
