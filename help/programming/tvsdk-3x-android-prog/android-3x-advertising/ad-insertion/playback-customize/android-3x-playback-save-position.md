---
description: Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
seo-description: Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
seo-title: Salvate la posizione del video e riprendete più tardi
title: Salvate la posizione del video e riprendete più tardi
uuid: cff1715e-c7a9-4eda-ad71-31892c3c1e78
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Salvate la posizione del video e riprendete più tardi {#save-the-video-position-and-resume-later}

Potete salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti dinamicamente differiscono tra le sessioni utente, pertanto il salvataggio della posizione **con** gli annunci a giunzione fa riferimento a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci in sequenza.

1. Quando l’utente esce da un video, l’applicazione recupera e salva la posizione nel video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni di annuncio possono variare in ogni sessione a causa di pattern di annunci, limiti di frequenza e così via. L’ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l&#39;applicazione recupera l&#39;ora locale, che è possibile salvare sul dispositivo o in un database sul server.

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `getCurrentTime` restituirà 1200 secondi, mentre `getLocalTime` a questa posizione restituiranno 900 secondi.

   >[!IMPORTANT]
   >
   >L&#39;ora locale e l&#39;ora corrente sono uguali per i flussi live/lineari. In questo caso, `convertToLocalTime` non ha effetto. Per VOD, l&#39;ora locale rimane invariata mentre gli annunci suonano.

   ```java
   // Save the user session when player activity stops 
       @Override 
       public void onStop(){ 
           super.onStop(); 
           ... 
           prefs = PreferenceManager.getDefaultSharedPreferences( 
                                     getActivity().getApplicationContext()); 
           SharedPreferences.Editor editor = prefs.edit(); 
           // get the local time where stream stopped playing and  
           // save it in System preferences 
           editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
           editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
           editor.commit(); 
           ... 
       }
   ```

1. Ripristinare la sessione utente quando l&#39;attività del lettore riprende.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs =  
         PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil"). 
         equals(_contentInfo.toMediaResource().getUrl())) { 
           _lastKnownLocalTime =  
             prefs.getLong(LAST_LOCAL_TIME, 0); // get the last local time  
                                                // saved in system preferences 
           if(_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. Per riprendere il video nella stessa posizione:

   * Per riprendere la riproduzione del video dalla posizione salvata da una sessione precedente, utilizzate `seekToLocalTime`.

      >[!TIP]
      >
      >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento non corretto.

   * Per cercare l&#39;ora corrente, utilizza `seek`.

1. Quando l&#39;applicazione riceve l&#39;evento `onStatusChanged` di modifica dello stato, cerca l&#39;ora locale salvata.

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if(_shouldResumePlayback){ 
               if(_lastKnownLocalTime >= 0) { 
                    _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
       ... 
   }
   ```

1. Specifica le interruzioni di annuncio come specificato nell&#39;interfaccia dei criteri di annuncio.
1. Implementa un selettore di criteri di annunci personalizzato estendendo il selettore di criteri di annunci predefinito.
1. Fornite le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`.

   Questo metodo include un&#39;interruzione annuncio pre-roll e le interruzioni annuncio mid-roll prima della posizione dell&#39;ora locale. L&#39;applicazione può decidere di riprodurre un&#39;interruzione di annuncio pre-roll e riprendere fino all&#39;ora locale specificata, di riprodurre un&#39;interruzione di annuncio mid-roll e riprendere fino all&#39;ora locale specificata, o di non riprodurre interruzioni di annuncio.