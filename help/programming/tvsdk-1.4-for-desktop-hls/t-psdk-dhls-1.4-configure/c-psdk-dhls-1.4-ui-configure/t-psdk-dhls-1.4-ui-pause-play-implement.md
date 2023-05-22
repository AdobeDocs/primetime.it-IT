---
description: È possibile aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
title: Riprodurre e mettere in pausa un video
exl-id: c1c259a4-edb8-475b-96a2-7fa0903804c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Riprodurre e mettere in pausa un video{#play-and-pause-a-video}

È possibile aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.

1. Creare un pulsante di pausa/riproduzione che esegua le operazioni seguenti.
   1. Attendi che il lettore sia almeno nello stato READY.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK:

      ```
      function play():void;
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo di pausa TVSDK:

      ```
      function pause():void;
      ```

1. Utilizza il callback per `MediaPlayerStatusChangeEvent.STATUS_CHANGED` per verificare la presenza di errori o per intraprendere altre azioni appropriate.

   TVSDK chiama questo callback quando viene chiamato il metodo di pausa o riproduzione. TVSDK trasmette informazioni sulla modifica dello stato nel callback, incluso il nuovo stato, ad esempio PAUSED o PLAY.
