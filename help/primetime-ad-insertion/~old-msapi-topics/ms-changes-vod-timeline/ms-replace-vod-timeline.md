---
description: La timeline dell’annuncio appropriata per una riproduzione del contenuto VOD potrebbe non essere appropriata per le riproduzioni successive. È possibile sostituire una timeline VOD senza modificare il contenuto.
title: Modifiche a VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Modifiche a VOD {#changes-to-vod}

La timeline dell’annuncio appropriata per una riproduzione del contenuto VOD potrebbe non essere appropriata per le riproduzioni successive. È possibile sostituire una timeline VOD senza modificare il contenuto.

Le situazioni in cui potresti voler sostituire una timeline VOD includono:

* Sostituisci gli annunci locali, ma lascia gli annunci nazionali durante una finestra C3.
* Sostituire gli annunci bruciati dopo la chiusura della finestra C3.
* Sostituisci dinamicamente i vecchi annunci C3 con annunci più recenti di durata maggiore.
* Inserisci un numero inferiore di annunci o nessun annuncio.

È possibile sostituire la timeline dell’annuncio inviando una nuova richiesta di inserimento dell’annuncio con il file M3U8 originale e un valore diverso di `pttimeline` parametro di query.