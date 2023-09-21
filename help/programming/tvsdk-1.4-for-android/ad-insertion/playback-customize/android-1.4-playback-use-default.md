---
description: Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.
title: Utilizza il comportamento di riproduzione predefinito
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Utilizza il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.

Per utilizzare i comportamenti predefiniti:

    * Se implementi la tua classe &quot;AdvertisingFactory&quot;, restituisce null per &quot;createAdPolicySelector&quot;.
    
    * Se non disponi di un’implementazione personalizzata per la classe &quot;AdvertisingFactory&quot;, TVSDK utilizza un selettore predefinito per i criteri degli annunci.
