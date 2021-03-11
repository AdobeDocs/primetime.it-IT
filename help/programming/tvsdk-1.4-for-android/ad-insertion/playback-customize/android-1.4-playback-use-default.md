---
description: Puoi scegliere di utilizzare i comportamenti degli annunci predefiniti.
title: Utilizzare il comportamento di riproduzione predefinito
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti degli annunci predefiniti.

Per utilizzare i comportamenti predefiniti:

    * Se implementi la tua classe `AdvertisingFactory`, restituisce null per `createAdPolicySelector` .
    
    * Se non disponi di un&#39;implementazione personalizzata per la classe &quot;AdvertisingFactory&quot;, TVSDK utilizza un selettore predefinito di criteri per gli annunci .