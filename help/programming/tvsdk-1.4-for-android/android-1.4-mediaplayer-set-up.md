---
description: L’interfaccia di MediaPlayer per Android racchiude le funzionalità e il comportamento di un lettore multimediale.
seo-description: L’interfaccia di MediaPlayer per Android racchiude le funzionalità e il comportamento di un lettore multimediale.
seo-title: Configurare MediaPlayer
title: Configurare MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configurare MediaPlayer {#set-up-the-mediaplayer}

L’interfaccia di MediaPlayer per Android racchiude le funzionalità e il comportamento di un lettore multimediale.

TVSDK fornisce un&#39;implementazione dell&#39; `MediaPlayer` interfaccia, la `DefaultMediaPlayer` classe. Per utilizzare la funzionalità di riproduzione video, create un’istanza `DefaultMediaPlayer`.

>[!TIP]
>
>Interagisci con l’ `DefaultMediaPlayer` istanza solo con i metodi esposti dall’ `MediaPlayer` interfaccia.

1. Create un&#39;istanza di MediaPlayer utilizzando il metodo `DefaultMediaPlayer.create` di fabbrica pubblico, passando un oggetto contestuale dell&#39;applicazione Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Chiamata `MediaPlayer.getView` per ottenere un riferimento all&#39; `MediaPlayerView` istanza.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Posizionate l&#39; `MediaPlayerView` istanza in un&#39; `FrameLayout` istanza, che posiziona il video sullo schermo del dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

L&#39; `MediaPlayer` istanza è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.
