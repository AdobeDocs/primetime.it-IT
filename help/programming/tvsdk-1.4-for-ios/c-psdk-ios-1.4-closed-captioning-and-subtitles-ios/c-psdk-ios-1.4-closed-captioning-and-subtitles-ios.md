---
description: I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.
seo-description: I sottotitoli e i sottotitoli codificati presentano differenze univoche e possono essere attivati in modi diversi.
seo-title: Sottotitoli e didascalie
title: Sottotitoli e didascalie
uuid: 91daf0be-087a-4be5-86c2-f8b83da43a8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Requisiti per i sottotitoli e i sottotitoli codificati {#requirements-for-subtitles-and-closed-captions}

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

      La `PTMediaPlayer` riproduce i contenuti principali e gli annunci, dove il contenuto principale potrebbe essere live/lineare o VOD, e gli annunci potrebbero essere pre-roll, mid-roll o post-roll.
   Di seguito sono riportati alcuni requisiti aggiuntivi per i sottotitoli in iOS:

   * Per le marche temporali, il `X-TIMESTAMP-MAP` valore specificato nella sezione di intestazione del `WebVTT` file deve corrispondere alla marca temporale del video.

   * Per il sistema, devi usare iOS 6.1 o versione successiva.


>[!IMPORTANT]
>
>I requisiti per i sottotitoli non si applicano ai sottotitoli codificati.

