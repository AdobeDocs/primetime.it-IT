---
description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
title: Selezionare una traccia di didascalia corrente tra le tracce disponibili
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Panoramica {#work-with-closed-captions}

I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l&#39;audio non è udibile o l&#39;utente non è udibile.

I sottotitoli codificati sono generalmente nella stessa lingua dell&#39;audio e presentano anche suoni in background come testo, ma in genere i sottotitoli sono in una lingua diversa e non includono suoni in background.

TVSDK supporta il rendering di questi formati:

* sottotitoli codificati 608 e 708, se distribuiti come parte del flusso di trasporto video su HLS come pacchetti di dati nei flussi video MPEG-2.
* File di sottotitoli WebVTT, a cui si fa riferimento dai file manifesto M3U8 come definiti nelle specifiche HLS. Sono automaticamente disponibili come brani di sottotitoli codificati nel lettore Primetime.

È possibile:

* Selezionate una traccia di didascalia disponibile come traccia corrente e ascoltate gli eventi che indicano tracce aggiuntive disponibili.
* Attivate o disattivate i sottotitoli (visibili o non visibili) utilizzando l&#39; `MediaPlayer` interfaccia.
* Selezionate le opzioni di stile che determinano il rendering dei sottotitoli codificati da parte del motore video sottostante. Utilizzare l&#39; `MediaPlayerItem` interfaccia per selezionare formati quali il font o il colore del font.
