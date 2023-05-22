---
description: L’interfaccia MediaPlayer per Android incapsula la funzionalità e il comportamento di un lettore multimediale.
title: Configurare MediaPlayer
exl-id: 2698fe8d-0b73-4aad-9fee-55d034d8ca64
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Configurare MediaPlayer {#set-up-the-mediaplayer}

L’interfaccia MediaPlayer per Android incapsula la funzionalità e il comportamento di un lettore multimediale.

TVSDK fornisce un’implementazione del `MediaPlayer` interfaccia, il `DefaultMediaPlayer` classe. Quando è necessaria la funzionalità di riproduzione video, crea un&#39;istanza `DefaultMediaPlayer`.

>[!TIP]
>
>Interagire con `DefaultMediaPlayer` solo con i metodi esposti dal `MediaPlayer` di rete.

1. Creare un&#39;istanza di MediaPlayer utilizzando il `DefaultMediaPlayer.create` metodo factory, passaggio di un oggetto di contesto dell&#39;applicazione Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Chiamata `MediaPlayer.getView` per ottenere un riferimento al `MediaPlayerView` dell&#39;istanza.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Posiziona `MediaPlayerView` istanza in una `FrameLayout` che inserisce il video sullo schermo del dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

Il `MediaPlayer` L’istanza di è ora disponibile e configurata correttamente per visualizzare contenuti video sullo schermo del dispositivo.
