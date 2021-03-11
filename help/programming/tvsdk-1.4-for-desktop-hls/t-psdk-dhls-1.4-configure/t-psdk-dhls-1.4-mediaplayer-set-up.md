---
description: L'interfaccia MediaPlayer incapsula le funzionalità e il comportamento di un lettore multimediale.
title: Configurare MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Configurare MediaPlayer {#set-up-the-mediaplayer}

TVSDK fornisce gli strumenti per la creazione di un’applicazione di lettore video avanzata (il lettore Primetime), che puoi integrare con altri componenti Primetime.

Utilizza gli strumenti della piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, TVSDK fornisce metodi di riproduzione e pausa. È possibile creare pulsanti dell&#39;interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi TVSDK.L&#39;interfaccia MediaPlayer incapsula le funzionalità e il comportamento di un lettore multimediale.

TVSDK fornisce un’unica implementazione dell’interfaccia `MediaPlayer` : Classe DefaultMediaPlayer. Quando hai bisogno della funzionalità di riproduzione video, crea un&#39;istanza `DefaultMediaPlayer`.

>[!NOTE]
>
>Interagisci con l&#39;istanza `DefaultMediaPlayer` solo con i metodi esposti dall&#39;interfaccia `MediaPlayer`.

1. Crea un&#39;istanza `MediaPlayerContext` utilizzando l&#39;istanza `authorizedFeatures` caricata dall&#39;applicazione (consulta [Carica il token firmato](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Creare un&#39;istanza di un oggetto `MediaPlayer` utilizzando il metodo create factory pubblico, passando un oggetto contestuale `MediaPlayerContext`:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   Questo restituisce un&#39;interfaccia `MediaPlayer` generica. 1. Crea un&#39;istanza `MediaPlayerView` e specifica l&#39;istanza StageVideo da utilizzare:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associa l’istanza `MediaPlayerView` alla visualizzazione appena creata:

   ```
   mediaPlayer.view = view;
   ```

1. Posiziona l’istanza `MediaPlayerView` sullo schermo del dispositivo:

   ```
   container.addChild(view)
   ```

L’istanza `MediaPlayer` è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.