---
description: Se il sistema dispone dell’accesso alla decodifica assistita dall’hardware, è possibile ottenere una riproduzione più fluida rispetto all’implementazione TVSDK del software puro utilizzando il formato iFrame.
seo-description: Se il sistema dispone dell’accesso alla decodifica assistita dall’hardware, è possibile ottenere una riproduzione più fluida rispetto all’implementazione TVSDK del software puro utilizzando il formato iFrame.
seo-title: Operazioni di gioco con i trucchi più semplici
title: Operazioni di gioco con i trucchi più semplici
uuid: 959d6c67-b64f-4666-8de7-54d247459fd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# Operazioni di gioco a tre tasti più fluide {#smoother-trick-play-operations}

Se il sistema dispone dell’accesso alla decodifica assistita dall’hardware, è possibile ottenere una riproduzione più fluida rispetto all’implementazione TVSDK del software puro utilizzando il formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

L’utilizzo del formato iFrame comporta operazioni di riproduzione con trucco non uniformi. Un&#39;operazione di riproduzione più fluida utilizza un profilo normale (non iFrame), il supporto della decodifica hardware e un frame rate più elevato. Diversi dispositivi di decodifica assistita da hardware hanno funzionalità diverse. La velocità doppia richiede 60 fotogrammi al secondo (FPS), mentre la velocità quadrupla richiede 120 FPS.

>[!IMPORTANT]
>
> Adobe consiglia di limitare la riproduzione alla velocità doppia per i dispositivi Android più recenti e di non utilizzare la funzione per i dispositivi Android meno recenti.

Per ottenere una riproduzione più fluida, impostare `ABRControlParameters.maxPlayoutRate` sul multiplo desiderato di velocità normale (ad esempio, 2.0 per la velocità doppia). Se una chiamata successiva a `MediaPlayer.setRate()` ha un argomento minore o uguale al valore impostato per `maxPlayoutRate`, TVSDK utilizza un profilo normale per ottenere una riproduzione più fluida. In caso contrario, utilizza un profilo iFrame per l’operazione trickplay.