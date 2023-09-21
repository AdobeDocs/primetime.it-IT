---
description: È possibile aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
title: Riprodurre e mettere in pausa un video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
