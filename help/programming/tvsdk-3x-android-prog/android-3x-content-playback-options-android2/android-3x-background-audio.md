---
seo-title: Abilitare l'audio in background
title: Abilitare l'audio in background
uuid: aa6dc934-e85c-4db1-901b-9777f47106e6
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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
