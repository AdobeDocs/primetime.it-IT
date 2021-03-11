---
description: Puoi usare TVSDK per recuperare informazioni sui file multimediali da visualizzare sulla barra di ricerca.
title: Visualizza la durata, l'ora corrente e il tempo rimanente del video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Visualizza la durata, l&#39;ora corrente e il tempo rimanente del video{#display-the-duration-current-time-and-remaining-time-of-the-video}

Puoi usare TVSDK per recuperare informazioni sui file multimediali da visualizzare sulla barra di ricerca.

1. Attendere che il lettore sia nello stato PREPARATO.
1. Recupera l&#39;ora corrente dell&#39;indicatore di riproduzione utilizzando il metodo `MediaPlayer.getCurrentTime` .

   Restituisce la posizione corrente dell&#39;indicatore di riproduzione sulla timeline virtuale, in millisecondi. Il tempo viene calcolato in base al flusso risolto che potrebbe contenere più istanze di contenuto alternativo, ad esempio più annunci o interruzioni pubblicitarie unite nel flusso principale. Per i flussi in tempo reale/lineare, il tempo restituito è sempre nell&#39;intervallo della finestra di riproduzione.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupera l&#39;intervallo di riproduzione del flusso e determina la sua durata.
   1. Utilizzare il metodo `mediaPlayer.getPlaybackRange` per ottenere l&#39;intervallo di tempo della timeline virtuale.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analizza l’intervallo di tempo utilizzando `mediacore.utils.TimeRange`.
   1. Per determinare la durata, sottraete l’inizio dalla fine dell’intervallo.

      Ciò include la durata del contenuto aggiuntivo inserito nel flusso (annunci).

      Per VOD, l’intervallo inizia sempre con zero e il valore finale è uguale alla somma della durata del contenuto principale e delle durate del contenuto aggiuntivo inserito nel flusso (annunci).

      Per una risorsa lineare/live, l’intervallo rappresenta l’intervallo della finestra di riproduzione e questo intervallo cambia durante la riproduzione.

      TVSDK chiama il callback `onUpdated` per indicare che l’elemento multimediale è stato aggiornato e che i relativi attributi (compreso l’intervallo di riproduzione) sono stati aggiornati.

1. Utilizza i metodi disponibili nella classe `MediaPlayer` e `SeekBar` che sono disponibili pubblicamente nell’SDK per Android per impostare i parametri della barra di ricerca.

   Ad esempio, ecco un possibile layout che contiene gli elementi `SeekBar` e due `TextView` .

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

   Nell&#39;esempio seguente viene utilizzata la classe di supporto `Clock.java` come timer, disponibile nel lettore di riferimento PrimetimeReference. Questa classe imposta un listener di eventi e attiva un evento `onTick` ogni secondo o un altro valore di timeout che è possibile specificare.

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

   Su ogni segno di spunta dell&#39;orologio, questo esempio recupera la posizione corrente del lettore multimediale e aggiorna SeekBar. Utilizza i due elementi TextView per contrassegnare l&#39;ora corrente e la posizione finale dell&#39;intervallo di riproduzione come valori numerici.

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

