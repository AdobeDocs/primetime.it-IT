---
description: La cronologia degli annunci appropriata per una riproduzione di contenuti VOD potrebbe non essere appropriata per le successive riproduzioni. Potete sostituire una timeline VOD senza modificare il contenuto.
seo-description: La cronologia degli annunci appropriata per una riproduzione di contenuti VOD potrebbe non essere appropriata per le successive riproduzioni. Potete sostituire una timeline VOD senza modificare il contenuto.
seo-title: Modifiche al VOD
title: Modifiche al VOD
uuid: e734aacd-b42e-4c8e-a16a-c7a0739a0492
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Modifiche al VOD {#changes-to-vod}

La cronologia degli annunci appropriata per una riproduzione di contenuti VOD potrebbe non essere appropriata per le successive riproduzioni. Potete sostituire una timeline VOD senza modificare il contenuto.

Le situazioni in cui si desidera sostituire una timeline VOD includono:

* Sostituire gli annunci locali, ma lasciare gli annunci nazionali durante una finestra C3.
* Sostituire gli annunci masterizzati dopo la chiusura della finestra di C3.
* Sostituisci dinamicamente vecchi annunci C3 con annunci più recenti di maggiore durata.
* Inserite un numero inferiore di annunci o nessuno.

Potete sostituire la timeline dell&#39;annuncio inviando una nuova richiesta di inserimento annunci con il file M3U8 originale e un valore diverso del parametro di query `pttimeline`.