---
description: Quando un utente fa clic su un annuncio, l'applicazione deve mettere in pausa la riproduzione del contenuto video principale.
seo-description: Quando un utente fa clic su un annuncio, l'applicazione deve mettere in pausa la riproduzione del contenuto video principale.
seo-title: Sospendi e riprendi riproduzione
title: Sospendi e riprendi riproduzione
uuid: 229e2499-e30e-458c-bd6d-d035588c21cf
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Sospendi e riprendi riproduzione {#pause-and-resume-playback}

Quando un utente fa clic su un annuncio, l&#39;applicazione deve mettere in pausa la riproduzione del contenuto video principale.

1. Ignorate le `onPause` e `onResume` dall&#39;attività Android.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```

