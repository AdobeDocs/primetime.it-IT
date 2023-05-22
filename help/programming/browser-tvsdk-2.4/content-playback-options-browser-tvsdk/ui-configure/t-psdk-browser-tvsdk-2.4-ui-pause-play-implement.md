---
description: È possibile aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.
title: Riprodurre e mettere in pausa un video
exl-id: ce3f8b0c-9765-4e77-b096-6b9789608fa8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Riprodurre e mettere in pausa un video{#play-and-pause-a-video}

È possibile aggiungere il comportamento TVSDK del browser per mettere in pausa e riprodurre i pulsanti.

1. Creare un pulsante di pausa/riproduzione che esegua le operazioni seguenti.
   1. Attendere che il lettore sia almeno nello stato PREPARATO.
   1. Per avviare la riproduzione, chiama il metodo di riproduzione TVSDK del browser:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Per mettere in pausa la riproduzione, chiama il metodo di pausa TVSDK del browser:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Ascolta la `AdobePSDK.MediaPlayerStatusChangeEvent` per verificare la presenza di errori o per intraprendere altre azioni appropriate.

   TVSDK del browser attiva questo evento quando vengono chiamati i metodi di pausa o riproduzione e trasmette informazioni sull’oggetto evento, incluso il nuovo stato, ad esempio `MediaPlayerStatus.PLAYING` o `MediaPlayerStatus.PAUSED`.
