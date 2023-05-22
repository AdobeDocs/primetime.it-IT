---
description: È possibile aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
title: Riprodurre e mettere in pausa un video
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Riprodurre e mettere in pausa un video{#play-and-pause-a-video}

È possibile aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.

1. Creare un pulsante di pausa/riproduzione che esegua le operazioni seguenti.
   1. Attendere che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo di pausa TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Utilizza il `MediaPlayer.PlaybackEventListener.onStateChanged` callback per verificare la presenza di errori o per eseguire altre azioni appropriate.

   TVSDK chiama questo callback quando viene chiamato il metodo di pausa o riproduzione. TVSDK trasmette informazioni sulla modifica dello stato nel callback, incluso il nuovo stato, ad esempio PAUSED o PLAY.
