---
description: L’interfaccia di MediaPlayer racchiude le funzionalità e il comportamento di un lettore multimediale.
seo-description: L’interfaccia di MediaPlayer racchiude le funzionalità e il comportamento di un lettore multimediale.
seo-title: Configurare MediaPlayer
title: Configurare MediaPlayer
uuid: 4b27643c-9ccd-4abb-9793-475d06ee2a88
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Configurare MediaPlayer {#set-up-the-mediaplayer}

TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime.

Utilizzate gli strumenti della piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, TVSDK fornisce metodi di riproduzione e pausa. È possibile creare pulsanti dell’interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi TVSDK.L’interfaccia di MediaPlayer racchiude le funzionalità e il comportamento di un lettore multimediale.

TVSDK fornisce un&#39;unica implementazione dell&#39; `MediaPlayer` interfaccia: la classe DefaultMediaPlayer. Per le funzioni di riproduzione video, create un’istanza `DefaultMediaPlayer`.

>[!NOTE]
>
>Interagisci con l’ `DefaultMediaPlayer` istanza solo con i metodi esposti dall’ `MediaPlayer` interfaccia.

1. Creare un&#39;istanza `MediaPlayerContext` utilizzando l&#39; `authorizedFeatures` istanza caricata dall&#39;applicazione (vedere [Caricare il token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)firmato).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Creare un&#39;istanza `MediaPlayer` utilizzando il metodo public create factory, passando un oggetto `MediaPlayerContext` contestuale:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Questo restituisce un&#39; `MediaPlayer` interfaccia generica. 1. Create un&#39;istanza `MediaPlayerView` e specificate l&#39;istanza StageVideo da utilizzare:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associate l’ `MediaPlayerView` istanza alla vista appena creata:

   ```
   mediaPlayer.view = view;
   ```

1. Posizionare l&#39; `MediaPlayerView` istanza sullo schermo del dispositivo:

   ```
   container.addChild(view)
   ```

L&#39; `MediaPlayer` istanza è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.