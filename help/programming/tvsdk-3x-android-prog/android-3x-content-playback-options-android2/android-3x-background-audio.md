---
title: Abilita audio di sfondo
description: Abilita audio di sfondo
copied-description: true
exl-id: 5bb72233-27d0-4968-b32c-c8d5ac5ac8c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Abilita audio di sfondo {#enable-background-audio}

Per abilitare la riproduzione audio quando l’app è in background, l’app deve chiamare `enableAudioPlaybackInBackground` API di MediaPlayer con argomento true come quando il lettore è nello stato PREPARATO.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

L’app deve mettere in pausa la riproduzione quando perde lo stato di attivazione audio durante eventi come la risposta al telefono, ecc. Il seguente frammento di codice illustra come implementare `OnAudioFocusChangeListener`:

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
