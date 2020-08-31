---
description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-title: Utilizzare il comportamento di riproduzione predefinito
title: Utilizzare il comportamento di riproduzione predefinito
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito{#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti annunci predefiniti.

Per utilizzare i comportamenti predefiniti:

* Se implementate la vostra `ContentFactory` classe, restituite una nuova istanza di `DefaultAdPolicySelector` nella vostra implementazione di `doRetrieveAdPolicySelector`.

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

* Se non disponete di un&#39;implementazione personalizzata per la `ContentFactory` classe, TVSDK utilizza `DefaultAdPolicySelector`.