---
description: Se StageVideo non è disponibile e l’applicazione tenta di utilizzare StageVideo, TVSDK non genera un errore. L'applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.
seo-description: Se StageVideo non è disponibile e l’applicazione tenta di utilizzare StageVideo, TVSDK non genera un errore. L'applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.
seo-title: Verificare la disponibilità di StageVideo
title: Verificare la disponibilità di StageVideo
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---


# Verificare se StageVideo è disponibile{#check-whether-stagevideo-is-available}

Se StageVideo non è disponibile e l’applicazione tenta di utilizzare StageVideo, TVSDK non genera un errore. L&#39;applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.

A partire dall&#39;Flash 15 e versioni successive, quando l&#39;hardware `StageVideo` non è disponibile, verrà ripristinato al software `StageVideo`. Ad Flash 14 e versioni precedenti, è possibile determinare se `StageVideo` è disponibile. Se `StageVideo` non è disponibile, è possibile utilizzare `StageVideoAvailabilityEvent` per capire perché non è disponibile.

1. Ascoltare `StageVideoAvailabilityEvent` per determinare se `StageVideo` è disponibile.

   Ad esempio:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Se `StageVideo` non è disponibile, controllare `flash.media.StageVideoAvailabilityReason`.
