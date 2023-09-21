---
description: Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 e il contenuto multimediale live inizia dal punto di attivazione del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.
title: Immettere un flusso in un momento specifico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Immettere un flusso in un momento specifico {#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 e il contenuto multimediale live inizia dal punto di attivazione del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.

   TVSDK considera la posizione specificata come punto di partenza della risorsa e non è richiesta alcuna operazione di ricerca. Se la posizione non è all&#39;interno dell&#39;intervallo ricercabile, TVSDK utilizza la posizione predefinita. Per ulteriori informazioni, consulta [Caricare una risorsa multimediale nel lettore multimediale](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

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
