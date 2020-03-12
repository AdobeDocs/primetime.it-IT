---
seo-title: Abilitare l'audio in background
title: Abilitare l'audio in background
uuid: 1e7319f5-ee16-47bd-bfd5-d3dcfe69bf4b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Abilitare l&#39;audio in background {#enable-background-audio}

Per abilitare la riproduzione audio quando l&#39;app è in background, l&#39;app deve chiamare `enableAudioPlaybackInBackground` API di MediaPlayer con true come argomento quando il lettore è in stato PREPARATO.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

L&#39;app deve mettere in pausa la riproduzione quando perde il blocco dell&#39;audio attivo durante eventi come la risposta al telefono, ecc. Il frammento di codice seguente illustra come implementare `OnAudioFocusChangeListener`:

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

