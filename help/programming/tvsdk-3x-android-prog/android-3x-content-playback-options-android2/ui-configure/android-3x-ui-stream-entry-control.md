---
description: Per impostazione predefinita, quando si avvia la riproduzione, il contenuto multimediale VOD inizia a 0 e il contenuto multimediale in tempo reale inizia dal punto live del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.
title: Immettere un flusso in un momento specifico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 1%

---


# Immettere un flusso in un momento specifico {#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, quando si avvia la riproduzione, il contenuto multimediale VOD inizia a 0 e il contenuto multimediale in tempo reale inizia dal punto live del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.

   TVSDK considera la posizione specificata come punto iniziale della risorsa e non è necessaria alcuna operazione di ricerca. Se la posizione non è all’interno dell’intervallo ricercabile, TVSDK utilizza la posizione predefinita. Per ulteriori informazioni, consulta [Caricare una risorsa multimediale nel lettore multimediale](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

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
