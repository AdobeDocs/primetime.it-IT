---
title: Pre-generazione delle licenze
description: Pre-generazione delle licenze
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Pre-generazione delle licenze{#pre-generating-licenses}

Se si stanno pregenerando licenze che contengono regole di utilizzo basate sul tempo, si consiglia vivamente che la licenza includa i requisiti di sincronizzazione (vedere *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti* ), in modo che la scadenza della licenza possa essere imposta in modo sicuro. L’implementazione di un meccanismo di &quot;heartbeat&quot; tra il client e il server è vivamente consigliata se nella licenza sono presenti restrizioni basate sul tempo, in quanto l’heartbeat sincronizzerà l’ora del client con quella del server.
