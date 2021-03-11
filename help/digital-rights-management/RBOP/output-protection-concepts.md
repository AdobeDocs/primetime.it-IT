---
description: Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell’output.
title: Concetti RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Concetti RBOP {#rbop-concepts}

Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell’output.

È possibile specificare i requisiti di protezione dell’output basati sulla risoluzione in una struttura JSON gerarchica. *I requisiti di output sono basati su pixel.*

Al livello più alto della specifica JSON, puoi definire la risoluzione massima dei pixel e i vincoli dei pixel per risoluzioni specifiche:

* `maxPixel` - La risoluzione massima dei pixel definisce la risoluzione massima per la quale si verificherà la decrittografia.
* `pixelConstraints` - I vincoli pixel definiscono i requisiti di output che devono essere applicati per una risoluzione specifica.

È possibile associare i requisiti di output a vincoli di pixel specifici. I tipi di requisiti che è possibile associare a un determinato vincolo di pixel includono restrizioni per le connessioni digitali, analogiche e OTA (over-the-air).

**Uscita digitale**

Il requisito dell&#39;uscita digitale può specificare opzioni restrittive, ad esempio &quot;è richiesta la protezione dell&#39;uscita digitale&quot; o &quot;la riproduzione non è consentita&quot;. I requisiti in materia di output possono inoltre specificare opzioni meno restrittive, ad esempio: &quot;nessuna protezione deve essere applicata&quot; o &quot;la protezione digitale deve essere utilizzata se disponibile&quot;.

**Uscita analogica**

Le connessioni di uscita analogiche sono più semplici dell&#39;uscita digitale; consistono in un unico requisito di uscita.
