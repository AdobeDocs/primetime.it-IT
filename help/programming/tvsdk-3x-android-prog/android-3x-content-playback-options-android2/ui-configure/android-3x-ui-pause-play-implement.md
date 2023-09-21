---
description: È possibile aggiungere pulsanti di pausa e riproduzione per mettere in pausa o riprodurre il video.
title: Riprodurre e mettere in pausa un video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Riprodurre e mettere in pausa un video {#play-and-pause-a-video}

È possibile aggiungere pulsanti di pausa e riproduzione per mettere in pausa o riprodurre il video.

1. Per creare un pulsante di pausa o riproduzione:
   1. Attendi che il lettore sia almeno nello stato preparato.
   1. Per avviare la riproduzione, chiamare il `play` metodo:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Per mettere in pausa la riproduzione, chiama `pause()` metodo:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilizza il callback dell&#39;evento di modifica dello stato per verificare la presenza di errori o per eseguire altre azioni appropriate.

   TVSDK chiama questo callback per `pause()` o `play()` e trasmette informazioni sulla modifica dello stato, incluso il nuovo stato, ad esempio in pausa o in riproduzione.
