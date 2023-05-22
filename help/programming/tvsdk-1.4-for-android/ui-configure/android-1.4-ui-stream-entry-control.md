---
description: Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.
title: Immettere un flusso in un momento specifico
exl-id: a16b6281-37d5-491c-a2d0-2090894c8a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Immettere un flusso in un momento specifico {#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.

   TVSDK considera la posizione specificata come punto di partenza della risorsa. Non è richiesta alcuna operazione di ricerca. Se la posizione non è all&#39;interno dell&#39;intervallo ricercabile, TVSDK utilizza la posizione predefinita.

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
