---
description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-title: Utilizzare il comportamento di riproduzione predefinito
title: Utilizzare il comportamento di riproduzione predefinito
uuid: ccda5223-17c1-4cda-b875-e706f5dc8648
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti annunci predefiniti.

Per utilizzare i comportamenti predefiniti:

    * Se si implementa la propria classe `AdvertisingFactory`, restituire null per `createAdPolicySelector`.
    
    * Se non disponete di un&#39;implementazione personalizzata per la classe &quot;AdvertisingFactory&quot;, TVSDK utilizza un selettore di criteri di annunci predefinito.