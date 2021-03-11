---
description: Quando manca un segmento, ad esempio quando un particolare segmento non viene scaricato, tenta di eseguire il ripristino tramite diversi tentativi di failover. Se non è in grado di eseguire il ripristino, viene generato un errore.
title: Failover dei segmenti mancante
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Failover dei segmenti mancante{#missing-segment-failover}

Quando manca un segmento, ad esempio quando un particolare segmento non viene scaricato, tenta di eseguire il ripristino tramite diversi tentativi di failover. Se non è in grado di eseguire il ripristino, viene generato un errore.

Se sul server manca un segmento perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover provando le seguenti opzioni:

1. Prova un failover sullo stesso segmento, allo stesso bit rate, in un file variante.
1. Passa a un bit rate alternativo (interruttore ABR) nello stesso file.
1. Scorrere ogni bit rate disponibile in ogni variante disponibile.
1. Ignora il segmento ed emette un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva una notifica di errore `CONTENT_ERROR`. Questa notifica contiene una notifica interna con il codice `DOWNLOAD_ERROR` . Se lo streaming con il problema è una traccia audio alternativa, genera la notifica di errore `AUDIO_TRACK_ERROR`.

Se il motore video non è in grado di ottenere continuamente i segmenti, limita l’salto continuo del segmento a 5, dopo di che la riproduzione viene interrotta ed emette un `NATIVE_ERROR` con il codice 5.

>[!NOTE]
>
>I parametri di controllo del bit rate adattivo (ABR) non vengono presi in considerazione quando si verifica un failover. Questo perché il meccanismo di failover è progettato per utilizzare come flussi di backup qualsiasi playlist attualmente disponibile, indipendentemente dal loro profilo bit-rate.
>
>Durante un&#39;operazione di failover, può essere presente uno switch di profilo. Se si verifica un errore durante il download di uno dei segmenti della playlist, i parametri di controllo ABR come il bit rate minimo/massimo consentito vengono ignorati.

