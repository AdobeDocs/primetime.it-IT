---
description: Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning.
title: Pubblicità
exl-id: 79ee4abf-a3f5-4915-ad4b-fe866acec882
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Pubblicità e sue esigenze {#advertising-requirements}

Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning.

Primetime ad decisioninglavora con TVSDK per identificare opportunità pubblicitarie, risolvere annunci e inserire annunci risolti nei flussi video.

Per incorporare gli annunci nel contenuto video, assicurati che il contenuto pubblicitario e il contenuto video principale soddisfino i seguenti requisiti:

* La versione HLS del contenuto pubblicitario non può essere superiore alla versione HLS del contenuto principale.
* Gli annunci non devono essere multiplexati (senza restrizioni), indipendentemente dal fatto che il contenuto principale sia multiplexato.
