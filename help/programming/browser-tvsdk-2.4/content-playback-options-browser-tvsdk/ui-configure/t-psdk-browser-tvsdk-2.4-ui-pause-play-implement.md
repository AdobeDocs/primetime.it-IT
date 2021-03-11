---
description: È possibile aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.
title: Riprodurre e mettere in pausa un video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Riprodurre e mettere in pausa un video{#play-and-pause-a-video}

È possibile aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.

1. Crea un pulsante di pausa/riproduzione che esegue le seguenti operazioni.
   1. Attendi che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK del browser:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo di pausa Browser TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Ascolta l’evento `AdobePSDK.MediaPlayerStatusChangeEvent` per verificare la presenza di errori o per intraprendere altre azioni appropriate.

   Il browser TVSDK attiva questo evento quando vengono chiamati i metodi di pausa o di riproduzione e trasmette informazioni sull&#39;oggetto evento, incluso il nuovo stato, ad esempio `MediaPlayerStatus.PLAYING` o `MediaPlayerStatus.PAUSED`.

