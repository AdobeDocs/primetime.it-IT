---
description: Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning. Primetime ad decisioninglavora con TVSDK per identificare opportunità pubblicitarie, risolvere annunci e inserire annunci risolti nei flussi video.
title: Requisiti pubblicitari
exl-id: 3ca82cc5-ed64-458e-9a8d-475a84512478
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Pubblicità e sue esigenze {#advertising-requirements}

Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning. Primetime ad decisioninglavora con TVSDK per identificare opportunità pubblicitarie, risolvere annunci e inserire annunci risolti nei flussi video.

<!--<a id="section_282A8000A8BF4860A24F0D3F1A19BC9E"></a>-->

Per incorporare gli annunci nel contenuto video, assicurati che il contenuto pubblicitario e il contenuto video principale soddisfino i seguenti requisiti:

* La versione HLS del contenuto pubblicitario non può essere superiore alla versione HLS del contenuto principale.
* Gli annunci non devono essere multiplexati (senza restrizioni), indipendentemente dal fatto che il contenuto principale sia multiplexato.
