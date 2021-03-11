---
description: I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.
title: Sottotitoli e sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Requisiti per sottotitoli e sottotitoli {#requirements-for-subtitles-and-closed-captions}

I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.

I flussi di sottotitoli vengono eseguiti in parallelo con il contenuto principale. I sottotitoli codificati fanno parte dei pacchetti di dati dei flussi video MPEG-2.

Per i sottotitoli e i sottotitoli codificati, tenere presente quanto segue:

* **Sottotitoli codificati**

   * I sottotitoli codificati si trovano in genere nella stessa lingua dell’audio e rappresentano anche i suoni in background come testo.
   * I sottotitoli codificati fanno parte dei pacchetti di dati dei flussi video MPEG-2 nel flusso di trasmissione video.
   * I sottotitoli codificati sono supportati nella misura fornita dal framework AV Foundation.

* **Sottotitoli**

   * I sottotitoli si trovano in una lingua diversa e non includono i suoni in background.
   * I sottotitoli si trovano in flussi che vengono eseguiti in parallelo con il contenuto principale.

      Il `PTMediaPlayer` riproduce il contenuto principale e gli annunci, dove il contenuto principale potrebbe essere live/lineare o VOD, e gli annunci potrebbero essere pre-roll, mid-roll o post-roll.
   Di seguito sono riportati alcuni requisiti aggiuntivi per i sottotitoli in iOS:

   * Per le marche temporali, il valore `X-TIMESTAMP-MAP`, specificato nella sezione di intestazione del file `WebVTT`, deve corrispondere alla marca temporale del video.

   * Per il sistema, devi utilizzare iOS 6.1 o versione successiva.


>[!IMPORTANT]
>
>I requisiti per i sottotitoli non si applicano ai sottotitoli codificati.

