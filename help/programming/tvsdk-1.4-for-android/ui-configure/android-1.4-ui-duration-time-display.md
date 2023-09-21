---
description: È possibile utilizzare TVSDK per recuperare informazioni sul supporto che è possibile visualizzare sulla barra di ricerca.
title: Visualizza la durata, l'ora corrente e il tempo rimanente del video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Visualizza la durata, l&#39;ora corrente e il tempo rimanente del video{#display-the-duration-current-time-and-remaining-time-of-the-video}

È possibile utilizzare TVSDK per recuperare informazioni sul supporto che è possibile visualizzare sulla barra di ricerca.

1. Attendere che il lettore sia nello stato PREPARATO.
1. Recupera il tempo corrente della testina di riproduzione utilizzando `MediaPlayer.getCurrentTime` metodo.

   Restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale in millisecondi. Il tempo viene calcolato rispetto al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci o interruzioni pubblicitarie unite nel flusso principale. Per i flussi live/lineari, il tempo restituito è sempre nell’intervallo della finestra di riproduzione.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupera l’intervallo di riproduzione del flusso e determina la durata.
   1. Utilizza il `mediaPlayer.getPlaybackRange` metodo per ottenere l’intervallo di tempo della timeline virtuale.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analizza l’intervallo di tempo utilizzando `mediacore.utils.TimeRange`.
   1. Per determinare la durata, sottrarre l&#39;inizio dalla fine dell&#39;intervallo.

      Ciò include la durata del contenuto aggiuntivo inserito nel flusso (annunci).

      Per VOD, l’intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo inserito nel flusso (annunci).

      Per una risorsa lineare/live, l’intervallo rappresenta l’intervallo della finestra di riproduzione e questo intervallo cambia durante la riproduzione.

      TVSDK chiama il tuo `onUpdated` callback per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi (incluso l’intervallo di riproduzione) sono stati aggiornati.

1. Utilizzare i metodi disponibili in `MediaPlayer` e `SeekBar` classe disponibile pubblicamente nell’SDK Android per impostare i parametri della barra di ricerca.

   Ad esempio, questo è un possibile layout che contiene `SeekBar` e due `TextView` elementi.

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

   Nell&#39;esempio seguente viene utilizzato `Clock.java` helper come timer, disponibile nel lettore di riferimento PrimetimeReference. Questa classe imposta un listener di eventi e attiva un `onTick` ogni secondo o un altro valore di timeout che puoi specificare.

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

   Ad ogni tick dell’orologio, questo esempio recupera la posizione corrente del lettore multimediale e aggiorna SeekBar. Vengono utilizzati i due elementi TextView per contrassegnare come valori numerici l&#39;ora corrente e la posizione finale dell&#39;intervallo di riproduzione.

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
