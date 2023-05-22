---
description: Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.
title: Utilizza il comportamento di riproduzione predefinito
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Utilizza il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.

Per utilizzare i comportamenti predefiniti:

    * Se implementi la tua classe &quot;AdvertisingFactory&quot;, restituisce null per &quot;createAdPolicySelector&quot;.
    
    * Se non disponi di un’implementazione personalizzata per la classe &quot;AdvertisingFactory&quot;, TVSDK utilizza un selettore predefinito per i criteri degli annunci.
