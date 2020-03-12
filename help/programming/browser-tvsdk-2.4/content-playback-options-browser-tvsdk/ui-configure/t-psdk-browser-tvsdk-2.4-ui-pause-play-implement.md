---
description: Potete aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.
seo-description: Potete aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.
seo-title: Riproduzione e pausa di un video
title: Riproduzione e pausa di un video
uuid: 4053ea9e-6b74-41e9-ad04-087ad13e3698
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Riproduzione e pausa di un video{#play-and-pause-a-video}

Potete aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.

1. Create un pulsante Pausa/Riproduci che esegua le seguenti operazioni.
   1. Aspettate che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK del browser:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Per mettere in pausa la riproduzione, chiamate il metodo Pausa TVSDK del browser:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Ascoltare l’ `AdobePSDK.MediaPlayerStatusChangeEvent` evento per verificare la presenza di errori o per eseguire altre azioni appropriate.

   Il browser TVSDK attiva questo evento quando i metodi pause o play vengono chiamati e trasmette informazioni sull&#39;oggetto evento, incluso il nuovo stato, ad esempio `MediaPlayerStatus.PLAYING` o `MediaPlayerStatus.PAUSED`.

