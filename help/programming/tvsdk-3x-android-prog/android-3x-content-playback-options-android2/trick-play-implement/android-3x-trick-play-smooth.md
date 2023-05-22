---
description: Se il sistema ha accesso alla decodifica assistita da hardware, puoi ottenere una riproduzione più fluida rispetto all’implementazione TVSDK del software puro utilizzando il formato iFrame.
title: Operazioni di riproduzione più semplici
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Operazioni di riproduzione più semplici {#smoother-trick-play-operations}

Se il sistema ha accesso alla decodifica assistita da hardware, puoi ottenere una riproduzione più fluida rispetto all’implementazione TVSDK del software puro utilizzando il formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

L&#39;utilizzo del formato iFrame consente di eseguire operazioni di riproduzione non uniformi. La riproduzione semplificata dei trucchi utilizza un profilo normale (non iFrame), supporto per la decodifica dell&#39;hardware e un frame rate più elevato. Diversi dispositivi di decodifica assistiti da hardware hanno funzionalità diverse. La doppia velocità richiede 60 fotogrammi al secondo (FPS) e la velocità quadrupla richiede 120 FPS.

>[!IMPORTANT]
>
>L’Adobe consiglia di limitare la riproduzione a una velocità doppia per i dispositivi Android più recenti e di non utilizzare la funzione per i dispositivi Android più vecchi.

Per ottenere una riproduzione più fluida, impostare `ABRControlParameters.maxPlayoutRate` al multiplo desiderato della velocità normale (ad esempio, 2,0 per velocità doppia). Se una chiamata successiva a `MediaPlayer.setRate()` ha un argomento minore o uguale al valore impostato per `maxPlayoutRate`, TVSDK utilizza un profilo normale per ottenere una riproduzione più fluida dei trucchi. In caso contrario, utilizza un profilo iFrame per l&#39;operazione di trickplay.
