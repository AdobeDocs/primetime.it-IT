---
description: L'interfaccia MediaPlayer per Android incapsula le funzionalità e il comportamento di un lettore multimediale.
title: Configurare MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Configurare MediaPlayer {#set-up-the-mediaplayer}

L&#39;interfaccia MediaPlayer per Android incapsula le funzionalità e il comportamento di un lettore multimediale.

TVSDK fornisce un’implementazione dell’interfaccia `MediaPlayer` , la classe `DefaultMediaPlayer` . Quando hai bisogno della funzionalità di riproduzione video, crea un&#39;istanza `DefaultMediaPlayer`.

>[!TIP]
>
>Interagisci con l&#39;istanza `DefaultMediaPlayer` solo con i metodi esposti dall&#39;interfaccia `MediaPlayer`.

1. Creare un&#39;istanza di MediaPlayer utilizzando il metodo di fabbrica pubblico `DefaultMediaPlayer.create`, passando un oggetto contestuale dell&#39;applicazione Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Chiama `MediaPlayer.getView` per ottenere un riferimento all&#39;istanza `MediaPlayerView`.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Posiziona l’istanza `MediaPlayerView` in un’istanza `FrameLayout`, che inserisce il video sullo schermo del dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

L’istanza `MediaPlayer` è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.
