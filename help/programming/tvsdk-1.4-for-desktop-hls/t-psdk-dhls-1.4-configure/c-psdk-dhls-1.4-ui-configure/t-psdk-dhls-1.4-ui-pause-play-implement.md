---
description: È possibile aggiungere un comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
title: Riprodurre e mettere in pausa un video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Riprodurre e mettere in pausa un video{#play-and-pause-a-video}

È possibile aggiungere un comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.

1. Crea un pulsante di pausa/riproduzione che esegue le seguenti operazioni.
   1. Attendi che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK:

      ```
      function play():void;
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo di pausa TVSDK:

      ```
      function pause():void;
      ```

1. Utilizza il callback per l&#39;evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` per verificare la presenza di errori o per intraprendere altre azioni appropriate.

   TVSDK chiama questo callback quando viene chiamato il metodo pause o play. TVSDK trasmette informazioni sulla modifica dello stato nel callback, incluso il nuovo stato, ad esempio PAUSED o PLAYING.
