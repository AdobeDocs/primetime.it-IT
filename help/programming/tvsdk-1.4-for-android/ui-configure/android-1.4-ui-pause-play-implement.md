---
description: Potete aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
seo-description: Potete aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.
seo-title: Riproduzione e pausa di un video
title: Riproduzione e pausa di un video
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Riproduzione e pausa di un video{#play-and-pause-a-video}

Potete aggiungere il comportamento TVSDK per mettere in pausa e riprodurre i pulsanti.

1. Create un pulsante Pausa/Riproduci che esegua le seguenti operazioni.
   1. Aspettate che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo TVSDK pause:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Utilizzate il `MediaPlayer.PlaybackEventListener.onStateChanged` callback per verificare la presenza di errori o per eseguire altre azioni appropriate.

   TVSDK chiama questo callback quando viene chiamato il metodo pause o play. TVSDK trasmette informazioni sulla modifica dello stato nel callback, incluso il nuovo stato, ad esempio PAUSED o PLAYING.

