---
description: Se il sistema ha accesso alla decodifica assistita dall'hardware, è possibile ottenere un gioco di trucco più semplice rispetto all'implementazione TVSDK del software puro utilizzando il formato iFrame.
title: Operazioni di gioco a trucco liscio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Operazioni di gioco con trucco più uniformi {#smoother-trick-play-operations}

Se il sistema ha accesso alla decodifica assistita dall&#39;hardware, è possibile ottenere un gioco di trucco più semplice rispetto all&#39;implementazione TVSDK del software puro utilizzando il formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

L&#39;utilizzo del formato iFrame comporta operazioni di riproduzione a trucco non uniformi. L&#39;utilizzo di funzioni di riproduzione a trucco è più semplice e utilizza un profilo normale (non iFrame), un supporto per la decodifica hardware e un frame rate più elevato. Diversi dispositivi di decodifica assistita da hardware hanno funzionalità diverse. La velocità doppia richiede 60 frame al secondo (FPS) e la velocità quadrupla richiede 120 FPS.

>[!IMPORTANT]
>
>Adobe consiglia di limitare la riproduzione a una velocità doppia per i dispositivi Android più recenti e di non utilizzare la funzione per i dispositivi Android meno recenti.

Per ottenere una riproduzione più fluida, impostate `ABRControlParameters.maxPlayoutRate` sul multiplo desiderato di velocità normale (ad esempio, 2.0 per la velocità doppia). Se una chiamata successiva a `MediaPlayer.setRate()` ha un argomento minore o uguale al valore impostato per `maxPlayoutRate`, TVSDK utilizza un profilo normale per ottenere una riproduzione più semplice. Altrimenti utilizza un profilo iFrame per l&#39;operazione trickplay.