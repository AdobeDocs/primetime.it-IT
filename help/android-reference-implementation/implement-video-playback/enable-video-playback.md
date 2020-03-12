---
description: Create un PlaybackManager che gestisca la configurazione del flusso HLS e l'operazione di riproduzione. Non è richiesta alcuna altra configurazione.
seo-description: Create un PlaybackManager che gestisca la configurazione del flusso HLS e l'operazione di riproduzione. Non è richiesta alcuna altra configurazione.
seo-title: Abilita riproduzione video
title: Abilita riproduzione video
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# Abilita riproduzione video {#enable-video-playback}

Create un PlaybackManager che gestisca la configurazione del flusso HLS e l&#39;operazione di riproduzione. Non è richiesta alcuna altra configurazione.

1. Creare l&#39;oggetto Media Player verificando che il codice seguente sia presente in [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. Create il manager di riproduzione tramite `ManagerFactory`:

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. Implementate l&#39; `PlaybackManagerEventListener` elemento in per gestire `PlayerFragment` gli eventi di riproduzione:

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. Registra il listener di eventi in `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. Impostare la risorsa video:

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. Configurate le operazioni della barra di controllo in `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## Documentazione API correlata {#related-api-documentation}

* [Class PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)