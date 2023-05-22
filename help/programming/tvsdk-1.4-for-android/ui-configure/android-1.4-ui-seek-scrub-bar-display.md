---
description: TVSDK supporta la ricerca in una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in streaming video on-demand (VOD) che live.
title: Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente
exl-id: 8076521b-579d-491f-97de-c7b57daa9b2e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca in una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in streaming video on-demand (VOD) che live.

>[!IMPORTANT]
>
>La ricerca in uno streaming live è consentita solo per DVR.

1. Imposta i callback per la ricerca.

       La ricerca è asincrona, pertanto TVSDK invia i seguenti eventi correlati alla ricerca:
   
   * `QOSEventListener.onSeekStart` - Ricerca iniziale.
   * `QOSEventListener.onSeekComplete` - Ricerca riuscita.
   * `QOSEventListener.onOperationFailed` - Ricerca non riuscita.

1. Attendi che il lettore si trovi in uno stato valido per la ricerca.

   Gli stati validi sono READY, COMPLETE, PAUSED e PLAY.

1. Utilizzare la barra di ricerca nativa per impostare `OnSeekBarChangeListener` per vedere quando l’utente esegue lo scorrimento.
1. Ascolta `QOSEventListener.onOperationFailed` e adotta le misure appropriate.

   Questo evento trasmette l’avviso appropriato. L’applicazione determina come procedere, ad esempio, tentando di nuovo la ricerca o continuando la riproduzione dalla posizione precedente.

1. Attendi che TVSDK chiami `QOSEventListener.onSeekComplete` callback.
1. Recuperate la posizione finale di riproduzione regolata utilizzando il parametro di posizione del callback.

   Questo è importante perché la posizione di inizio effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Il comportamento di riproduzione potrebbe essere influenzato se una ricerca o un altro riposizionamento termina al centro di un’interruzione pubblicitaria o salta un’interruzione pubblicitaria.

1. Utilizzare le informazioni sulla posizione quando si visualizza una barra di scorrimento di ricerca.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Esempio di ricerca**

In questo esempio, l’utente pulisce la barra di ricerca per cercare la posizione desiderata.

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
