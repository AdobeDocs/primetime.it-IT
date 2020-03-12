---
description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-description: I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l'audio non è udibile o l'utente non è udibile.
seo-title: Utilizzo dei sottotitoli codificati
title: Utilizzo dei sottotitoli codificati
uuid: 6e105316-a166-45c1-b6b0-70c89c97c297
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Panoramica {#work-with-closed-captions-overview}

I sottotitoli codificati visualizzano la parte audio di un video come testo sullo schermo quando l&#39;audio non è udibile o l&#39;utente non è udibile.

I sottotitoli codificati sono generalmente nella stessa lingua dell&#39;audio e presentano anche suoni in background come testo, ma in genere i sottotitoli sono in una lingua diversa e non includono suoni in background.

TVSDK supporta il rendering di questi formati:

* sottotitoli codificati 608 e 708, se distribuiti come parte del flusso di trasporto video su HLS come pacchetti di dati nei flussi video MPEG-2.
* File di sottotitoli WebVTT, a cui si fa riferimento dai file manifesto M3U8 come definiti nelle specifiche HLS.

   Questi file sono automaticamente disponibili come tracce di sottotitoli codificati nel lettore Primetime.

Potete effettuare le seguenti operazioni:

* Selezionate una traccia di didascalia disponibile come traccia corrente e ascoltate gli eventi che indicano tracce aggiuntive disponibili.
* Attivate (visibile) o disattivate (non visibile) i sottotitoli codificati mediante l’ `MediaPlayer` interfaccia.
* Selezionate le opzioni di stile che determinano il rendering dei sottotitoli codificati da parte del motore video sottostante.

   Utilizzare l&#39; `MediaPlayerItem` interfaccia per selezionare formati quali il font o il colore del font.

