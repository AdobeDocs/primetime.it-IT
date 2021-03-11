---
description: TVSDK supporta la ricerca di una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, in video on demand (VOD) e flussi live.
title: Visualizza una barra di scorrimento con la posizione di riproduzione corrente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Visualizzare una barra di scorrimento con la posizione di riproduzione corrente {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca di una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, in video on demand (VOD) e flussi live.

>[!TIP]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Imposta i callback per la ricerca.

       La ricerca è asincrona, quindi TVSDK invia i seguenti eventi relativi alla ricerca:
   
   * `MediaPlayerEvent.SEEK_BEGIN`, dove inizia la ricerca.
   * `MediaPlayerEvent.SEEK_END`, dove la ricerca ha successo.
   * `MediaPlayerEvent.OPERATION_FAILED`, dove la ricerca ha fallito.

1. Attendi che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATO, COMPLETO, PAUSED e PLAYING.
1. Utilizza il `SeekBar` nativo per impostare `OnSeekBarChangeListener`, che determina quando l&#39;utente esegue il lavaggio.
1. Passa la posizione di ricerca richiesta (millisecondi) al metodo `MediaPlayer.seek` .

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Puoi cercare solo nella durata ricercabile della risorsa. Per i video on demand, da 0 a la durata della risorsa.

   >[!TIP]
   >
   >Questo passaggio sposta la testina di riproduzione in una nuova posizione nel flusso, ma la posizione calcolata finale potrebbe differire dalla posizione di ricerca specificata.

1. Ascolta `MediaPlayerEvent.OPERATION_FAILED` e adotta le azioni appropriate.

   Questo evento trasmette l&#39;avviso appropriato. L&#39;applicazione determina come procedere e le opzioni includono provare di nuovo la ricerca o continuare la riproduzione dalla posizione precedente.

1. Attendi che TVSDK chiami il callback `MediaPlayerEvent.SEEK_END` .
1. Recupera la posizione di riproduzione regolata finale utilizzando il parametro di posizione del callback.

   Questo è importante perché la posizione iniziale effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Le regole, compreso il comportamento di riproduzione, sono influenzate se si può applicare una ricerca o un altro riposizionamento al centro di un’interruzione pubblicitaria o salta interruzioni pubblicitarie.

1. Utilizza le informazioni sulla posizione quando visualizzi una barra di scorrimento della ricerca.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Esempio di ricerca**

In questo esempio, l’utente sposta la barra di ricerca per cercare nella posizione desiderata.

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()), 
        playbackRange.getDuration()); 
     
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```

