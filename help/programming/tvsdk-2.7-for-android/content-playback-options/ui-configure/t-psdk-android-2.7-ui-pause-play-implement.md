---
description: È possibile aggiungere pulsanti di pausa e riproduzione per mettere in pausa o riprodurre il video.
title: Riprodurre e mettere in pausa un video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Riprodurre e mettere in pausa un video {#play-and-pause-a-video}

È possibile aggiungere pulsanti di pausa e riproduzione per mettere in pausa o riprodurre il video.

1. Per creare un pulsante di pausa o di riproduzione:
   1. Attendi che il lettore sia almeno nello stato preparato.
   1. Per avviare la riproduzione, chiama il metodo `play` :

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo `pause()` :

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilizza il callback dell’evento modificato per verificare la presenza di errori o per intraprendere altre azioni appropriate.

   TVSDK chiama questo callback per `pause()` o `play()` e trasmette informazioni sulla modifica dello stato, incluso il nuovo stato, ad esempio in pausa o in riproduzione.

