---
description: TVSDK supporta la ricerca in una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, in flussi video on-demand (VOD) e live.
title: Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca in una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, in flussi video on-demand (VOD) e live.

>[!TIP]
>
>La ricerca in uno streaming live è consentita solo per DVR.

1. Imposta i callback per la ricerca.

       La ricerca è asincrona, pertanto TVSDK invia i seguenti eventi correlati alla ricerca:
   
   * `MediaPlayerEvent.SEEK_BEGIN`, dove inizia la ricerca.
   * `MediaPlayerEvent.SEEK_END`, dove la ricerca ha esito positivo.
   * `MediaPlayerEvent.OPERATION_FAILED`, in cui la ricerca non è riuscita.

1. Attendi che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono READY, COMPLETE, PAUSED e PLAYED.
1. Utilizza il file nativo `SeekBar` per impostare `OnSeekBarChangeListener`, che determina quando l’utente esegue lo scorrimento.
1. Passa la posizione di ricerca richiesta (millisecondi) al `MediaPlayer.seek` metodo.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Puoi eseguire la ricerca solo nella durata della risorsa ricercabile. Per il video on-demand, va da 0 alla durata della risorsa.

   >[!TIP]
   >
   >Questo passaggio sposta la testina di riproduzione in una nuova posizione nel flusso, ma la posizione finale calcolata potrebbe differire dalla posizione di ricerca specificata.

1. Ascolta `MediaPlayerEvent.OPERATION_FAILED` e adotta le misure appropriate.

   Questo evento trasmette l’avviso appropriato. L’applicazione determina come procedere e le opzioni includono il tentativo di eseguire nuovamente la ricerca o continuare la riproduzione dalla posizione precedente.

1. Attendi che TVSDK chiami `MediaPlayerEvent.SEEK_END` callback.
1. Recuperate la posizione finale di riproduzione regolata utilizzando il parametro di posizione del callback.

   Questo è importante perché la posizione di inizio effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Potrebbero essere applicate le regole, incluso il comportamento di riproduzione, se una ricerca o un altro riposizionamento termina al centro di un’interruzione pubblicitaria o salta interruzioni pubblicitarie.

1. Utilizzare le informazioni sulla posizione quando si visualizza una barra di scorrimento di ricerca.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Esempio di ricerca**

In questo esempio, l’utente pulisce la barra di ricerca per cercare la posizione desiderata.

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
