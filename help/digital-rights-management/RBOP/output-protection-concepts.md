---
description: Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell'output.
seo-description: Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell'output.
seo-title: Concetti RBOP
title: Concetti RBOP
uuid: fc19c3c9-39a1-4b62-b763-101e5454a01f
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Concetti RBOP {#rbop-concepts}

Questa sezione fornisce una panoramica concettuale della configurazione, delle opzioni e dei significati associati alla protezione dell&#39;output.

I requisiti di protezione dell&#39;output basati sulla risoluzione vengono specificati in una struttura JSON gerarchica. *I requisiti di output sono basati su pixel.*

Al livello più alto della specifica JSON, potete definire la risoluzione massima in pixel e i vincoli in pixel per risoluzioni specifiche:

* `maxPixel` - La risoluzione massima in pixel definisce la risoluzione massima per la quale si verificherà la decrittazione.
* `pixelConstraints` - I vincoli pixel definiscono i requisiti di output che devono essere applicati per una risoluzione specificata.

Potete associare i requisiti di output a specifici vincoli di pixel. I tipi di requisiti che è possibile associare a un determinato vincolo di pixel includono restrizioni per le connessioni digitali, analogiche e OTA.

**Uscita digitale**

Il requisito dell&#39;uscita digitale può specificare opzioni restrittive, ad esempio &quot;è richiesta una protezione dell&#39;uscita digitale&quot; o &quot;la riproduzione non è consentita&quot;. I requisiti di output possono inoltre specificare opzioni meno restrittive, ad esempio &quot;nessuna protezione dovrebbe essere applicata&quot; o &quot;la protezione digitale dovrebbe essere utilizzata se disponibile&quot;.

**Uscita analogica**

Le connessioni di uscita analogiche sono più semplici dell&#39;uscita digitale; consistono in un unico requisito di uscita.
