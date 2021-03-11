---
description: TVSDK supporta la ricerca di una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in video on demand (VOD) che in streaming live.
title: Visualizza una barra di scorrimento con la posizione di riproduzione corrente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Visualizzare una barra di scorrimento con la posizione di riproduzione corrente {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca di una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in video on demand (VOD) che in streaming live.

>[!IMPORTANT]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Imposta i callback per la ricerca.

       La ricerca è asincrona, quindi TVSDK invia i seguenti eventi relativi alla ricerca:
   
   * `QOSEventListener.onSeekStart` - Cercare di iniziare.
   * `QOSEventListener.onSeekComplete` - Cercare di successo.
   * `QOSEventListener.onOperationFailed` - Ricerca non riuscita.

1. Attendi che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATI, COMPLETI, SOSPESI e RIPRODUZIONE.

1. Utilizzare SeekBar nativo per impostare `OnSeekBarChangeListener` per vedere quando l&#39;utente sta eseguendo il lavaggio.
1. Ascolta `QOSEventListener.onOperationFailed` e adotta le azioni appropriate.

   Questo evento trasmette l&#39;avviso appropriato. L&#39;applicazione determina come procedere, ad esempio, provando di nuovo la ricerca o continuando la riproduzione dalla posizione precedente.

1. Attendi che TVSDK chiami il callback `QOSEventListener.onSeekComplete` .
1. Recupera la posizione di riproduzione regolata finale utilizzando il parametro di posizione del callback.

   Questo è importante perché la posizione iniziale effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Il comportamento di riproduzione potrebbe essere interessato se una ricerca o un altro riposizionamento termina al centro di un&#39;interruzione pubblicitaria o salta interruzioni pubblicitarie.

1. Utilizza le informazioni sulla posizione quando visualizzi una barra di scorrimento della ricerca.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Esempio di ricerca**

In questo esempio, l’utente sposta la barra di ricerca per cercare nella posizione desiderata.

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
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

