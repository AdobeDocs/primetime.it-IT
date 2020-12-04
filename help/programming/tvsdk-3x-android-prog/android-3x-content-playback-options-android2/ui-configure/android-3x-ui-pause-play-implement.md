---
description: Potete aggiungere i pulsanti Pausa e Riproduci per mettere in pausa o riprodurre il video.
seo-description: Potete aggiungere i pulsanti Pausa e Riproduci per mettere in pausa o riprodurre il video.
seo-title: Riproduzione e pausa di un video
title: Riproduzione e pausa di un video
uuid: 3778a1fb-929c-4579-a14c-561179473dea
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Riproduzione e pausa di un video {#play-and-pause-a-video}

Potete aggiungere i pulsanti Pausa e Riproduci per mettere in pausa o riprodurre il video.

1. Per creare un pulsante di pausa o di riproduzione:
   1. Aspettate che il lettore sia almeno nello stato preparato.
   1. Per avviare la riproduzione, chiamare il metodo `play`:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Per mettere in pausa la riproduzione, chiamate il metodo `pause()`:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Utilizzate il callback dell&#39;evento modificato di stato per verificare la presenza di errori o per eseguire altre azioni appropriate.

   TVSDK chiama questo callback per `pause()` o `play()` e trasmette informazioni sulla modifica dello stato, incluso il nuovo stato, ad esempio in pausa o in riproduzione.