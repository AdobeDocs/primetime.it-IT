---
description: L’interfaccia MediaPlayer incapsula la funzionalità e il comportamento di un lettore multimediale.
title: Configurare MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Configurare MediaPlayer {#set-up-the-mediaplayer}

TVSDK fornisce gli strumenti per creare un’applicazione video player avanzata (il lettore Primetime), che puoi integrare con altri componenti di Primetime.

Utilizza gli strumenti della tua piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, TVSDK fornisce metodi di riproduzione e pausa. È possibile creare pulsanti dell&#39;interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi TVSDK.L&#39;interfaccia MediaPlayer incapsula la funzionalità e il comportamento di un lettore multimediale.

TVSDK fornisce un’unica implementazione del `MediaPlayer` interface: classe DefaultMediaPlayer. Quando è necessaria la funzionalità di riproduzione video, crea un&#39;istanza `DefaultMediaPlayer`.

>[!NOTE]
>
>Interagire con `DefaultMediaPlayer` solo con i metodi esposti da `MediaPlayer` di rete.

1. Crea istanza di `MediaPlayerContext` utilizzando l&#39;applicazione caricata `authorizedFeatures` istanza (vedere [Carica il token firmato](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Crea istanza di `MediaPlayer` utilizzando il metodo public create factory, passando un `MediaPlayerContext` oggetto di contesto:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Restituisce un valore generico `MediaPlayer` di rete. 1. Creare un’istanza di `MediaPlayerView` e specificare l&#39;istanza StageVideo da utilizzare:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associa `MediaPlayerView` istanza con la visualizzazione appena creata:

   ```
   mediaPlayer.view = view;
   ```

1. Posiziona `MediaPlayerView` istanza sullo schermo del dispositivo:

   ```
   container.addChild(view)
   ```

Il `MediaPlayer` L’istanza di è ora disponibile e configurata correttamente per visualizzare contenuti video sullo schermo del dispositivo.
