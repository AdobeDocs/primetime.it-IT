---
description: Potete aggiungere i pulsanti Pausa e Riproduci per mettere in pausa o riprodurre il video.
seo-description: Potete aggiungere i pulsanti Pausa e Riproduci per mettere in pausa o riprodurre il video.
seo-title: Riproduzione e pausa di un video
title: Riproduzione e pausa di un video
uuid: 66fefead-7f1d-46ed-a23e-381f25697978
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Riproduzione e pausa di un video {#play-and-pause-a-video}

Potete aggiungere i pulsanti Pausa e Riproduci per mettere in pausa o riprodurre il video.

1. Per creare un pulsante di pausa o di riproduzione:
   1. Aspettate che il lettore sia almeno nello stato preparato.
   1. Per avviare la riproduzione, chiamate il `play` metodo:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Per mettere in pausa la riproduzione, chiamate il `pause()` metodo:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilizzate il callback dell&#39;evento modificato di stato per verificare la presenza di errori o per eseguire altre azioni appropriate.

   TVSDK chiama questo callback `pause()` o `play()` trasmette informazioni sulla modifica dello stato, incluso il nuovo stato, ad esempio in pausa o in riproduzione.

