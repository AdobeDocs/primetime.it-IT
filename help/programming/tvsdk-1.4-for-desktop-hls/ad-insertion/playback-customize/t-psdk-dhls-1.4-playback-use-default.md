---
description: Puoi scegliere di utilizzare i comportamenti degli annunci predefiniti.
title: Utilizzare il comportamento di riproduzione predefinito
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito{#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti degli annunci predefiniti.

Per utilizzare i comportamenti predefiniti:

* Se implementi la tua classe `ContentFactory`, restituisce una nuova istanza di `DefaultAdPolicySelector` nell&#39;implementazione di `doRetrieveAdPolicySelector`.

   ```
   public class CustomContentFactory extends ContentFactory { 
   
       //... 
       // your custom code for advertising classes 
       //... 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function  
         doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new DefaultAdPolicySelector(item); 
       } 
   }
   ```

* Se non disponi di un’implementazione personalizzata per la classe `ContentFactory` , TVSDK utilizza `DefaultAdPolicySelector`.