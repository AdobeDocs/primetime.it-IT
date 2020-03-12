---
description: Potete usare TVSDK per recuperare informazioni sui file multimediali che potete visualizzare sulla barra di ricerca.
seo-description: Potete usare TVSDK per recuperare informazioni sui file multimediali che potete visualizzare sulla barra di ricerca.
seo-title: Visualizzare la durata, l’ora corrente e il tempo rimanente del video
title: Visualizzare la durata, l’ora corrente e il tempo rimanente del video
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Visualizzare la durata, l’ora corrente e il tempo rimanente del video{#display-the-duration-current-time-and-remaining-time-of-the-video}

Potete usare TVSDK per recuperare informazioni sui file multimediali che potete visualizzare sulla barra di ricerca.

1. Aspettate che il lettore sia nello stato PREPARATO.
1. Recuperare il tempo corrente dell&#39;indicatore di riproduzione utilizzando il `MediaPlayer.getCurrentTime` metodo .

   Questo restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale, in millisecondi. L&#39;ora viene calcolata in relazione al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci pubblicitari o interruzioni di annunci nel flusso principale. Per i flussi live/lineari, il tempo restituito è sempre compreso nell&#39;intervallo della finestra di riproduzione.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recuperate l’intervallo di riproduzione del flusso e stabilite la durata.
   1. Utilizzare il `mediaPlayer.getPlaybackRange` metodo per ottenere l&#39;intervallo di tempo della cronologia virtuale.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analizzare l&#39;intervallo di tempo utilizzando `mediacore.utils.TimeRange`.
   1. Per determinare la durata, sottraete l’inizio dalla fine dell’intervallo.

      Ciò include la durata del contenuto aggiuntivo inserito nel flusso (annunci).

      Per il VOD, l&#39;intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo inserito nel flusso (annunci).

      Per una risorsa lineare/live, l&#39;intervallo rappresenta l&#39;intervallo della finestra di riproduzione e questo intervallo cambia durante la riproduzione.

      TVSDK chiama il `onUpdated` callback per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi (incluso l’intervallo di riproduzione) sono stati aggiornati.

1. Utilizzate i metodi disponibili nell’SDK per Android `MediaPlayer` e nella `SeekBar` classe che sono disponibili pubblicamente per impostare i parametri della barra di ricerca.

   Ad esempio, di seguito è riportato un layout possibile che contiene gli `SeekBar` e due `TextView` elementi.

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

1. Utilizzare un timer per recuperare periodicamente l&#39;ora corrente e aggiornare SeekBar.

   L&#39;esempio seguente utilizza la classe `Clock.java` helper come timer, disponibile nel lettore di riferimento PrimetimeReference. Questa classe imposta un listener di eventi e attiva un `onTick` evento ogni secondo, o un altro valore di timeout che è possibile specificare.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   Su ogni tasto di clock, questo esempio recupera la posizione corrente del lettore multimediale e aggiorna SeekBar. Utilizza i due elementi TextView per contrassegnare l&#39;ora corrente e la posizione finale dell&#39;intervallo di riproduzione come valori numerici.

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```

