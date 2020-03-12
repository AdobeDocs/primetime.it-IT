---
description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-title: Inserire un flusso in un momento specifico
title: Inserire un flusso in un momento specifico
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Inserire un flusso in un momento specifico {#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.

   TVSDK considera la posizione specificata come punto di partenza per la risorsa e non è richiesta alcuna operazione di ricerca. Se la posizione non è all’interno dell’intervallo ricercabile, TVSDK utilizza la posizione predefinita. Per ulteriori informazioni, consultate [Caricare una risorsa multimediale nel lettore](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)multimediale.

   Ad esempio:

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```
