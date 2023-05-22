---
description: Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell'output.
title: Concetti RBOP
exl-id: 5b9de292-e060-467d-beca-5f428e45ed69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Concetti RBOP {#rbop-concepts}

Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell&#39;output.

I requisiti di protezione dell’output basati sulla risoluzione vengono specificati in una struttura JSON gerarchica. *I requisiti di uscita sono basati su pixel.*

Al livello più alto della specifica JSON, puoi definire la risoluzione massima in pixel e i vincoli in pixel per le risoluzioni specificate:

* `maxPixel` - La risoluzione pixel massima definisce la risoluzione massima per la quale si verifica la decrittografia.
* `pixelConstraints` - I vincoli di pixel definiscono i requisiti di output che devono essere applicati per una risoluzione specificata.

Associate i requisiti di output a specifici vincoli di pixel. I tipi di requisiti che è possibile associare a un determinato vincolo di pixel includono le restrizioni per le connessioni digitali, analogiche e over-the-air (OTA).

**Uscita digitale**

Il requisito dell&#39;uscita digitale può specificare opzioni restrittive, ad esempio &quot;è necessaria la protezione dell&#39;uscita digitale&quot; o &quot;la riproduzione non è consentita&quot;. I requisiti di uscita possono inoltre specificare opzioni meno restrittive, ad esempio &quot;non deve essere applicata alcuna protezione&quot; o &quot;deve essere utilizzata la protezione digitale, se disponibile&quot;.

**Uscita analogica**

Le connessioni di uscita analogica sono più semplici dell&#39;uscita digitale e consistono in un&#39;unica uscita.
