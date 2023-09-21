---
description: Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.
title: Utilizza il comportamento di riproduzione predefinito
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Utilizza il comportamento di riproduzione predefinito{#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.

Per utilizzare i comportamenti predefiniti:

* Se implementi un `ContentFactory` classe, restituisce una nuova istanza di `DefaultAdPolicySelector` nell&#39;implementazione di `doRetrieveAdPolicySelector`.

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

* Se non hai un’implementazione personalizzata per `ContentFactory` classe, TVSDK utilizza `DefaultAdPolicySelector`.
