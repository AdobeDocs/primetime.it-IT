---
description: I sottotitoli codificati visualizzano la parte audio di un video sotto forma di testo sullo schermo quando l’audio non è udibile o l’utente non è udito.
title: Utilizzare i sottotitoli codificati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Panoramica {#work-with-closed-captions-overview}

I sottotitoli codificati visualizzano la parte audio di un video sotto forma di testo sullo schermo quando l’audio non è udibile o l’utente non è udito.

I sottotitoli codificati si trovano in genere nella stessa lingua dell’audio e presentano anche suoni di sottofondo come testo, ma in genere i sottotitoli sono in una lingua diversa e non includono suoni di sottofondo.

TVSDK supporta il rendering di questi formati:

* sottotitoli codificati 608 e 708, se forniti come parte del flusso di trasporto video su HLS come pacchetti di dati in flussi video MPEG-2.
* File di didascalie WebVTT, a cui si fa riferimento dai file manifest M3U8 come definiti nelle specifiche HLS.

   Questi file sono automaticamente disponibili come tracce di sottotitoli nel lettore Primetime.

Puoi effettuare le seguenti operazioni:

* Selezionare una traccia di didascalia disponibile come traccia corrente e ascoltare gli eventi che indicano ulteriori tracce disponibili.
* Attiva (visibile) o disattiva (non visibile) i sottotitoli codificati mediante l’interfaccia `MediaPlayer`.
* Selezionare le opzioni di stile che determinano il rendering dei sottotitoli codificati da parte del motore video sottostante.

   Utilizza l&#39;interfaccia `MediaPlayerItem` per selezionare formati quali il colore del font o del font.

