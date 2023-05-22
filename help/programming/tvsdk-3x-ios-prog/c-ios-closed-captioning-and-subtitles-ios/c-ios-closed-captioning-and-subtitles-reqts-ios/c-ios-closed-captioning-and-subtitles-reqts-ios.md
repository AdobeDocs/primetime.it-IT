---
description: I sottotitoli codificati e i sottotitoli presentano alcune differenze uniche e possono essere attivati in modi diversi.
title: Requisiti relativi ai sottotitoli e ai sottotitoli codificati
exl-id: f90dcfb7-4fd2-41d5-8396-cdc827f8a8c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Requisiti relativi ai sottotitoli e ai sottotitoli codificati {#requirements-for-subtitles-and-closed-captions}

I sottotitoli codificati e i sottotitoli presentano alcune differenze uniche e possono essere attivati in modi diversi.

I flussi di sottotitoli vengono eseguiti in parallelo con il contenuto principale. I sottotitoli codificati fanno parte dei pacchetti di dati dei flussi video MPEG-2.

Devi conoscere i seguenti requisiti per i sottotitoli codificati e i sottotitoli:

* **Sottotitoli**

   * I sottotitoli codificati sono in genere nella stessa lingua dell&#39;audio e rappresentano anche i suoni di sottofondo come testo.
   * I sottotitoli codificati fanno parte dei pacchetti di dati dei flussi video MPEG-2 nel flusso di trasmissione video.
   * I sottotitoli codificati sono supportati nella misura fornita dal framework di AV Foundation.

* **Sottotitoli**

   * I sottotitoli sono in genere in una lingua diversa e non includono i suoni di sottofondo.
   * I sottotitoli sono in flussi che vengono eseguiti in parallelo al contenuto principale.

      Il `PTMediaPlayer` riproduce il contenuto principale e gli annunci, dove il contenuto principale potrebbe essere live/lineare o VOD, e gli annunci potrebbero essere pre-roll, mid-roll o post-roll.
   Di seguito sono riportati alcuni requisiti aggiuntivi per i sottotitoli in iOS:

   * Per i timestamp, `X-TIMESTAMP-MAP` valore specificato nella sezione dell&#39;intestazione del `WebVTT` deve corrispondere al timestamp del video.

   * Per il sistema, è necessario utilizzare iOS 6.1 o versione successiva.


>[!IMPORTANT]
>
>I requisiti relativi ai sottotitoli non si applicano ai sottotitoli codificati.
