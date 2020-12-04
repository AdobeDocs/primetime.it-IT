---
description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-description: Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-title: Inserire un flusso in un momento specifico
title: Inserire un flusso in un momento specifico
uuid: ac3479e2-46a1-4ac8-a9e8-68a23f5dd74d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 1%

---


# Immettere un flusso in un momento specifico {#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, quando si avvia la riproduzione, il supporto VOD inizia da 0 (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.

   TVSDK considera la posizione specificata come punto di partenza per la risorsa. Non è richiesta alcuna operazione di ricerca. Se la posizione non è all’interno dell’intervallo ricercabile, TVSDK utilizza la posizione predefinita.

   Ad esempio:

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   ```

