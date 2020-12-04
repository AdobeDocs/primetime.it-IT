---
description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-title: Inserire un flusso in un momento specifico
title: Inserire un flusso in un momento specifico
uuid: 65a19192-b890-4d69-9cb1-582a22988d2b
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# Immettere un flusso in un momento specifico {#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.

   TVSDK considera la posizione specificata come punto di partenza per la risorsa e non è richiesta alcuna operazione di ricerca. Se la posizione non è all’interno dell’intervallo ricercabile, TVSDK utilizza la posizione predefinita. Per ulteriori informazioni, vedere [Caricare una risorsa multimediale nel lettore multimediale](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

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

