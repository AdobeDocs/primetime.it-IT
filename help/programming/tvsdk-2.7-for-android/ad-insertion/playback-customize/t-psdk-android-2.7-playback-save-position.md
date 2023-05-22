---
description: È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.
title: Salva la posizione del video e riprendi in un secondo momento
exl-id: 6b1eeeeb-ae13-437f-80cc-1ceb7bf8ac19
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Salva la posizione del video e riprendi in un secondo momento {#save-the-video-position-and-resume-later}

È possibile salvare la posizione di riproduzione corrente in un video e riprendere la riproduzione nella stessa posizione in una sessione futura.

Gli annunci inseriti in modo dinamico differiscono tra le sessioni utente, pertanto la posizione viene salvata **con** gli annunci uniti si riferiscono a una posizione diversa in una sessione futura. TVSDK fornisce metodi per recuperare la posizione di riproduzione ignorando gli annunci uniti.

1. Quando l’utente chiude un video, l’applicazione recupera e salva la posizione all’interno del video.

   >[!TIP]
   >
   >Le durate degli annunci non sono incluse.

   Le interruzioni pubblicitarie possono variare in ogni sessione a causa di modelli di annunci, limiti di frequenza e così via. L’ora corrente del video in una sessione potrebbe essere diversa in una sessione futura. Quando si salva una posizione nel video, l&#39;applicazione recupera l&#39;ora locale, che è possibile salvare sul dispositivo o in un database sul server.

   Ad esempio, se l’utente si trova al 20° minuto del video e questa posizione include cinque minuti di annunci, `getCurrentTime` restituirà 1200 secondi, mentre `getLocalTime` in questa posizione restituirà 900 secondi.

   >[!IMPORTANT]
   >
   >L’ora locale e l’ora corrente sono le stesse per i flussi live/lineari. In questo caso, `convertToLocalTime` non ha alcun effetto. Per VOD, l’ora locale rimane invariata durante la riproduzione degli annunci.

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

1. Ripristina la sessione utente quando l’attività del lettore riprende.

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

   * Per riprendere la riproduzione del video dalla posizione salvata da una sessione precedente, utilizzare `seekToLocalTime`.

      >[!TIP]
      >
      >Questo metodo viene chiamato solo con valori di ora locali. Se il metodo viene chiamato con i risultati dell&#39;ora corrente, si verifica un comportamento errato.

   * Per cercare fino all&#39;ora corrente, utilizzare `seek`.

1. Quando l&#39;applicazione riceve `onStatusChanged` evento di modifica dello stato, cerca nell’ora locale salvata.

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

1. Specifica le interruzioni pubblicitarie come specificato nell’interfaccia dei criteri relativi agli annunci.
1. Implementa un selettore di criteri per annunci personalizzato estendendo il selettore di criteri per annunci predefinito.
1. Fornisci le interruzioni pubblicitarie che devono essere presentate all&#39;utente implementando `selectAdBreaksToPlay`.

   Questo metodo include un’interruzione pubblicitaria pre-roll e le interruzioni pubblicitarie mid-roll prima della posizione temporale locale. L’applicazione può decidere di riprodurre un’interruzione pubblicitaria pre-roll e riprendere all’ora locale specificata, riprodurre un’interruzione pubblicitaria mid-roll e riprendere all’ora locale specificata oppure non riprodurre interruzioni pubblicitarie.
