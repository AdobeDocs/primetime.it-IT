---
description: Quando un utente fa clic su un annuncio, l'applicazione deve mettere in pausa la riproduzione del contenuto video principale.
seo-description: Quando un utente fa clic su un annuncio, l'applicazione deve mettere in pausa la riproduzione del contenuto video principale.
seo-title: Sospendi e riprendi riproduzione
title: Sospendi e riprendi riproduzione
uuid: a8fec392-3a71-4086-abf1-23522d023680
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Sospendi e riprendi riproduzione {#pause-and-resume-playback}

Quando un utente fa clic su un annuncio, l&#39;applicazione deve mettere in pausa la riproduzione del contenuto video principale.

Ignorate le `onPause` e `onResume` dall&#39;attività Android.

```java
@Override 
public void onResume() { 
    super.onResume(); 
    requestAudioFocus(); 
    if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
        _mediaPlayer.play(); 
    } 
} 
... 
 
@Override 
public void onPause() { 
    super.onPause(); 
    if (_mediaPlayer != null) { 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
          _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
            _savedPlayerState = _mediaPlayer.getStatus(); 
            _lastKnownTime = _mediaPlayer.getCurrentTime(); 
        } 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
            _mediaPlayer.pause(); 
            _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
        } 
    } 
} 
 
abandonAudioFocus(); 
```

