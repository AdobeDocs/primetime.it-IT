---
description: Se StageVideo non è disponibile e l'applicazione tenta di utilizzare StageVideo, TVSDK non genera un errore. L'applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.
title: Verifica se StageVideo è disponibile
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Verifica se StageVideo è disponibile{#check-whether-stagevideo-is-available}

Se StageVideo non è disponibile e l&#39;applicazione tenta di utilizzare StageVideo, TVSDK non genera un errore. L&#39;applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.

Dal Flash 15 in poi, quando l&#39;hardware `StageVideo` non è disponibile, tornerà al software `StageVideo`. Per il Flash 14 e versioni precedenti, è possibile determinare se `StageVideo` è disponibile. Se `StageVideo` non è disponibile, è possibile utilizzare `StageVideoAvailabilityEvent` per capire perché non è disponibile.

1. Ascolta `StageVideoAvailabilityEvent` per determinare se `StageVideo` è disponibile.

   Ad esempio:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Se `StageVideo` non è disponibile, seleziona `flash.media.StageVideoAvailabilityReason`.
