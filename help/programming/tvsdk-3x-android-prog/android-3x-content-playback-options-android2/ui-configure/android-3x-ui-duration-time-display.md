---
description: Puoi usare TVSDK per recuperare informazioni sulla posizione del lettore nel supporto e visualizzarlo sulla barra di ricerca.
title: Visualizza la durata, l'ora corrente e il tempo rimanente del video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Visualizza la durata, l&#39;ora corrente e il tempo rimanente del video {#display-the-duration-current-time-and-remaining-time-of-the-video}

Puoi usare TVSDK per recuperare informazioni sulla posizione del lettore nel supporto e visualizzarlo sulla barra di ricerca.

1. Attendere che il lettore sia almeno nello stato PREPARATO.
1. Recupera il tempo corrente della testina di riproduzione utilizzando `MediaPlayer.getCurrentTime` metodo.

   Restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale in millisecondi. Il tempo viene calcolato rispetto al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci o interruzioni pubblicitarie unite nel flusso principale. Per i flussi live/lineari, il tempo restituito è sempre nell’intervallo della finestra di riproduzione.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Recupera l’intervallo di riproduzione del flusso e determina la durata.
   1. Utilizza il `MediaPlayer.getPlaybackRange` metodo per ottenere l’intervallo di tempo della timeline virtuale.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Utilizza il `MediaPlayer.getPlaybackRange` metodo per ottenere l’intervallo di tempo della timeline virtuale.

      * Per VOD, l’intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo nel flusso (annunci).
      * Per una risorsa lineare/live, l’intervallo rappresenta l’intervallo della finestra di riproduzione. Questo intervallo cambia durante la riproduzione.

        TVSDK chiama `ITEM_Updated` callback per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi, incluso l’intervallo di riproduzione, sono stati aggiornati.

1. Utilizza i metodi disponibili in `MediaPlayer` e il `SeekBar` nell&#39;SDK per Android per impostare i parametri della barra di ricerca.

   Ad esempio, questo è un possibile layout che contiene la barra di ricerca e due `TextView` elementi.

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. Usate un timer per recuperare periodicamente l&#39;ora corrente e aggiornare la barra di ricerca, come mostrato nella figura:

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   Nell&#39;esempio seguente viene utilizzato `Clock.java` classe helper, disponibile in `ReferencePlayer`, come timer. Questa classe imposta un listener di eventi e attiva un `onTick` ogni secondo o un altro valore di timeout che puoi specificare.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   Ad ogni tick dell’orologio, questo esempio recupera la posizione corrente del lettore multimediale e aggiorna la barra di ricerca. Utilizza i due `TextView` elementi per contrassegnare come valori numerici l’ora corrente e la posizione finale dell’intervallo di riproduzione.

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
