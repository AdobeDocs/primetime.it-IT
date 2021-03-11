---
title: Licenze di pregenerazione
description: Licenze di pregenerazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Licenze di pre-generazione{#pre-generating-licenses}

Se stai pregenerando licenze che contengono regole di utilizzo basate su tempo, si consiglia vivamente che la licenza includa requisiti di sincronizzazione (consulta *Utilizzo dell’SDK per Adobe Access per la protezione dei contenuti* guida), in modo che la scadenza della licenza possa essere applicata in modo sicuro. L&#39;implementazione di un meccanismo &quot;heartbeat&quot; tra il client e il server è altamente consigliato se si dispone di restrizioni basate sul tempo nella licenza, poiché il battito cardiaco sincronizzerà l&#39;ora del client con l&#39;ora del server.
