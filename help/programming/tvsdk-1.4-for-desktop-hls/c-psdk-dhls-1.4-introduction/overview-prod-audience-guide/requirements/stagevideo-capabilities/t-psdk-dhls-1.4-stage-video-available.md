---
description: Se StageVideo non è disponibile e l'applicazione tenta di utilizzare StageVideo, il TVSDK non genera un errore. L'applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.
title: Verifica se StageVideo è disponibile
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Verifica se StageVideo è disponibile{#check-whether-stagevideo-is-available}

Se StageVideo non è disponibile e l&#39;applicazione tenta di utilizzare StageVideo, il TVSDK non genera un errore. L&#39;applicazione può determinare se StageVideo è disponibile ascoltando StageVideoAvailabilityEvent.

A partire dal Flash 15 e versioni successive, quando l&#39;hardware `StageVideo` non è disponibile, rientrerà nel software `StageVideo`. Per i Flash 14 e precedenti, è possibile determinare se `StageVideo` è disponibile. Se `StageVideo` non è disponibile, è possibile utilizzare `StageVideoAvailabilityEvent` per comprendere perché non è disponibile.

1. Ascolta `StageVideoAvailabilityEvent` per determinare se `StageVideo` è disponibile.

   Ad esempio:

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. Se `StageVideo` non è disponibile, selezionare `flash.media.StageVideoAvailabilityReason`.
