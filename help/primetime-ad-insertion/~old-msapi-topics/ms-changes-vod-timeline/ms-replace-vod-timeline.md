---
description: La timeline dell’annuncio appropriata per una riproduzione di contenuti VOD può essere inappropriata per le successive riproduzioni. È possibile sostituire una timeline VOD senza modificare il contenuto.
title: Modifiche al VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Modifiche al VOD {#changes-to-vod}

La timeline dell’annuncio appropriata per una riproduzione di contenuti VOD può essere inappropriata per le successive riproduzioni. È possibile sostituire una timeline VOD senza modificare il contenuto.

Le situazioni in cui si desidera sostituire una timeline VOD includono:

* Sostituire gli annunci locali, ma lasciare gli annunci nazionali durante una finestra C3.
* Sostituire gli annunci bruciati dopo la chiusura della finestra C3.
* Sostituisci dinamicamente vecchi annunci C3 con annunci più recenti di maggiore durata.
* Inserisci meno annunci o nessuno.

Puoi sostituire la timeline dell’annuncio inviando una nuova richiesta di inserimento annuncio con il file M3U8 originale e un valore diverso del parametro di query `pttimeline` .