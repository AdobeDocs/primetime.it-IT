---
description: Potete aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
seo-description: Potete aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
seo-title: Riproduzione e pausa di un video
title: Riproduzione e pausa di un video
uuid: 04b3b23f-5ef1-4cc4-a22f-f6ffa9cefce5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Riproduzione e pausa di un video{#play-and-pause-a-video}

Potete aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.

1. Create un pulsante Pausa/Riproduci che esegua le seguenti operazioni.
   1. Aspettate che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK:

      ```
      function play():void;
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo TVSDK pause:

      ```
      function pause():void;
      ```

1. Utilizzate il callback per l&#39; `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento per verificare la presenza di errori o per eseguire altre azioni appropriate.

   TVSDK chiama questo callback quando viene chiamato il metodo pause o play. TVSDK trasmette informazioni sulla modifica dello stato nel callback, incluso il nuovo stato, ad esempio PAUSED o PLAYING.
