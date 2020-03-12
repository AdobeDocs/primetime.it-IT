---
description: È possibile utilizzare TVSDK per recuperare informazioni sulla posizione del lettore nel supporto e visualizzarlo sulla barra di ricerca.
seo-description: È possibile utilizzare TVSDK per recuperare informazioni sulla posizione del lettore nel supporto e visualizzarlo sulla barra di ricerca.
seo-title: Visualizzare la durata, l’ora corrente e il tempo rimanente del video
title: Visualizzare la durata, l’ora corrente e il tempo rimanente del video
uuid: 29bb6bc2-dab1-4f35-abcf-d3213605ee70
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visualizzare la durata, l’ora corrente e il tempo rimanente del video {#display-the-duration-current-time-and-remaining-time-of-the-video}

È possibile utilizzare TVSDK per recuperare informazioni sulla posizione del lettore nel supporto e visualizzarlo sulla barra di ricerca.

1. Attendere che il lettore sia almeno nello stato PREPARATO.
1. Recuperare il tempo corrente dell&#39;indicatore di riproduzione utilizzando il `MediaPlayer.getCurrentTime` metodo .

   Questo restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale, in millisecondi. L&#39;ora viene calcolata in relazione al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci pubblicitari o interruzioni di annunci nel flusso principale. Per i flussi live/lineari, il tempo restituito è sempre compreso nell&#39;intervallo della finestra di riproduzione.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Recuperate l’intervallo di riproduzione del flusso e stabilite la durata.
   1. Utilizzare il `MediaPlayer.getPlaybackRange` metodo per ottenere l&#39;intervallo di tempo della cronologia virtuale.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Utilizzare il `MediaPlayer.getPlaybackRange` metodo per ottenere l&#39;intervallo di tempo della cronologia virtuale.

      * Per il VOD, l&#39;intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo nel flusso (annunci).
      * Per una risorsa lineare/live, l&#39;intervallo rappresenta l&#39;intervallo delle finestre di riproduzione. Questo intervallo cambia durante la riproduzione.

         TVSDK chiama il `ITEM_Updated` callback per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi, incluso l’intervallo di riproduzione, sono stati aggiornati.

1. Utilizzate i metodi disponibili su `MediaPlayer` e sulla `SeekBar` classe nell’SDK Android per impostare i parametri della barra di ricerca.

   Ad esempio, di seguito è riportato un layout possibile che contiene la barra di ricerca e due `TextView` elementi.

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

1. Utilizzare un timer per recuperare periodicamente l&#39;ora corrente e aggiornare la barra di ricerca, come mostrato nella figura:

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width=&quot;477.000pt&quot;}

   Nell&#39;esempio seguente viene utilizzata la classe `Clock.java` helper, disponibile in `ReferencePlayer`, come timer. Questa classe imposta un listener di eventi e attiva un `onTick` evento ogni secondo, o un altro valore di timeout che è possibile specificare.

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

   Ad ogni clic dell&#39;orologio, questo esempio recupera la posizione corrente del lettore multimediale e aggiorna la barra di ricerca. Utilizza i due `TextView` elementi per contrassegnare l’ora corrente e la posizione finale dell’intervallo di riproduzione come valori numerici.

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
