---
description: I sottotitoli codificati visualizzano la porzione audio di un video come testo sullo schermo quando l'audio non è udibile o lo spettatore è ipoudente.
title: Utilizzare i sottotitoli
exl-id: e93725e3-6c6d-42b8-83d0-0feb4f9be50b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Panoramica {#work-with-closed-captions-overview}

I sottotitoli codificati visualizzano la porzione audio di un video come testo sullo schermo quando l&#39;audio non è udibile o lo spettatore è ipoudente.

I sottotitoli codificati sono in genere nella stessa lingua dell&#39;audio e visualizzano anche i suoni di sottofondo come testo, ma i sottotitoli sono in genere in una lingua diversa e non includono i suoni di sottofondo.

TVSDK supporta il rendering dei seguenti formati:

* 608 e 708 sottotitoli, se forniti come parte del flusso di trasporto video su HLS come pacchetti di dati in flussi video MPEG-2.
* File di didascalia WebVTT, a cui si fa riferimento dai file manifesto M3U8 definiti nelle specifiche HLS.

   Questi file sono automaticamente disponibili come tracce di sottotitoli nel lettore Primetime.

È possibile effettuare le seguenti operazioni:

* Selezionare un brano di didascalia disponibile come brano corrente e ascoltare gli eventi che indicano altri brani disponibili.
* Attiva (visibile) o disattiva (non visibile) i sottotitoli utilizzando `MediaPlayer` di rete.
* Seleziona le opzioni di stile che determinano il rendering dei sottotitoli codificati da parte del motore video sottostante.

   Utilizza il `MediaPlayerItem` per selezionare formati quali il carattere o il colore del carattere.
