---
description: I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.
seo-description: I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.
seo-title: Requisiti per i sottotitoli e i sottotitoli codificati
title: Requisiti per i sottotitoli e i sottotitoli codificati
uuid: 18ed6ac1-4b25-4590-8c61-3ffb0464d093
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Requisiti per sottotitoli e didascalie {#requirements-for-subtitles-and-closed-captions}

I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.

I flussi di sottotitoli vengono eseguiti in parallelo con il contenuto principale. I sottotitoli codificati fanno parte dei pacchetti di dati dei flussi video MPEG-2.

Per i sottotitoli e i sottotitoli codificati, tenete presente quanto segue:

* **Sottotitoli codificati**

   * I sottotitoli codificati sono generalmente nella stessa lingua dell&#39;audio e rappresentano anche l&#39;audio in background come testo.
   * I sottotitoli codificati fanno parte dei pacchetti di dati dei flussi video MPEG-2 nel flusso di trasmissione video.
   * I sottotitoli codificati sono supportati nella misura fornita dal framework AV Foundation.

* **Sottotitoli**

   * I sottotitoli sono in genere in una lingua diversa e non includono i suoni in background.
   * I sottotitoli si trovano in flussi che vengono eseguiti in parallelo con il contenuto principale.

      Il `PTMediaPlayer` riproduce il contenuto principale e gli annunci, dove il contenuto principale potrebbe essere live/lineare o VOD, e gli annunci potrebbero essere pre-roll, mid-roll o post-roll.
   Di seguito sono riportati alcuni requisiti aggiuntivi per i sottotitoli in iOS:

   * Per le marche temporali, il valore `X-TIMESTAMP-MAP`, specificato nella sezione di intestazione del file `WebVTT`, deve corrispondere alla marca temporale del video.

   * Per il sistema, devi usare iOS 6.1 o versione successiva.


>[!IMPORTANT]
>
>I requisiti per i sottotitoli non si applicano ai sottotitoli codificati.