---
description: Quando un utente fa clic su un annuncio, l'applicazione deve mettere in pausa la riproduzione del contenuto video principale.
seo-description: Quando un utente fa clic su un annuncio, l'applicazione deve mettere in pausa la riproduzione del contenuto video principale.
seo-title: Sospendi e riprendi riproduzione
title: Sospendi e riprendi riproduzione
uuid: 87ba9f05-912d-4b85-8add-feb26a796a3a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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

