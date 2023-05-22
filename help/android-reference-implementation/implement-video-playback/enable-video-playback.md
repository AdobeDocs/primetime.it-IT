---
description: Creare un oggetto PlaybackManager che gestisca la configurazione del flusso HLS e l'operazione di riproduzione. Non è richiesta alcuna altra configurazione.
title: Abilita riproduzione video
exl-id: b53f602b-5752-4471-9905-2e4351dfc8d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Abilita riproduzione video {#enable-video-playback}

Creare un oggetto PlaybackManager che gestisca la configurazione del flusso HLS e l&#39;operazione di riproduzione. Non è richiesta alcuna altra configurazione.

1. Crea l’oggetto lettore multimediale verificando che in sia presente il seguente codice [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. Creare la gestione della riproduzione tramite `ManagerFactory`:

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. Implementare `PlaybackManagerEventListener` nel `PlayerFragment` per gestire gli eventi di riproduzione:

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. Registrare il listener di eventi in `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. Configura la risorsa video:

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. Impostare le operazioni della barra di controllo in `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## Documentazione API correlata {#related-api-documentation}

* [Class Playback Manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)
