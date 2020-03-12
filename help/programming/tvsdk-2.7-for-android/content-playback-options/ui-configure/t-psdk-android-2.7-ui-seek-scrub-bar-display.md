---
description: TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, in video on demand (VOD) e flussi live.
seo-description: TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, in video on demand (VOD) e flussi live.
seo-title: Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente
title: Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente
uuid: df045a10-8d74-4874-8fa5-7e9571c8678d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, in video on demand (VOD) e flussi live.

>[!TIP]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Configurare le callback per la ricerca.

       La ricerca è asincrona, pertanto TVSDK invia i seguenti eventi relativi alla ricerca:
   
   * `MediaPlayerEvent.SEEK_BEGIN`, dove inizia la ricerca.
   * `MediaPlayerEvent.SEEK_END`, dove la ricerca ha esito positivo.
   * `MediaPlayerEvent.OPERATION_FAILED`, dove la ricerca non è riuscita.

1. Attendere che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATO, COMPLETO, SOSPESO E RIPRODUZIONE.
1. Utilizzate l&#39;elemento nativo `SeekBar` per impostare `OnSeekBarChangeListener`, che determina quando l&#39;utente esegue il trascinamento.
1. Passa la posizione di ricerca richiesta (millisecondi) al `MediaPlayer.seek` metodo.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Potete effettuare ricerche solo nella durata della risorsa. Per i video su richiesta, ossia da 0 alla durata della risorsa.

   >[!TIP]
   >
   >Questo passaggio sposta l&#39;indicatore di riproduzione in una nuova posizione nel flusso, ma la posizione calcolata finale potrebbe essere diversa dalla posizione di ricerca specificata.

1. Ascoltare `MediaPlayerEvent.OPERATION_FAILED` e intraprendere le azioni appropriate.

   Questo evento supera l&#39;avviso appropriato. L&#39;applicazione determina come procedere e le opzioni includono provare di nuovo la ricerca o continuare la riproduzione dalla posizione precedente.

1. Attendi che TVSDK chiami il `MediaPlayerEvent.SEEK_END` callback.
1. Recuperate la posizione di riproduzione rettificata finale utilizzando il parametro di posizione del callback.

   Questo è importante perché la posizione iniziale effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Le regole, incluso il comportamento di riproduzione, vengono influenzate se è possibile che una ricerca o un altro riposizionamento termini al centro di un&#39;interruzione dell&#39;annuncio o salti interruzioni dell&#39;annuncio.

1. Utilizzate le informazioni sulla posizione quando visualizzate una barra di scorrimento della ricerca.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Esempio di ricerca**

In questo esempio, l&#39;utente scorre la barra di ricerca per cercare la posizione desiderata.

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

