---
description: TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, sia nei flussi video on demand (VOD) che in quelli live.
seo-description: TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, sia nei flussi video on demand (VOD) che in quelli live.
seo-title: Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente
title: Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente
uuid: a9f4dd6c-78cf-455c-8c31-b2f7b740d84a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente {#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, sia nei flussi video on demand (VOD) che in quelli live.

>[!IMPORTANT]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Configurare le callback per la ricerca.

       La ricerca è asincrona, pertanto TVSDK invia i seguenti eventi relativi alla ricerca:
   
   * `QOSEventListener.onSeekStart` - Cercare di iniziare.
   * `QOSEventListener.onSeekComplete` - Cercare di successo.
   * `QOSEventListener.onOperationFailed` - Ricerca non riuscita.

1. Attendere che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATI, COMPLETI, SOSPESI E RIPRODUZIONE.

1. Utilizzate la barra di ricerca nativa per impostare `OnSeekBarChangeListener` in modo da visualizzare quando l&#39;utente sta eseguendo il trascinamento.
1. Ascoltare `QOSEventListener.onOperationFailed` e intraprendere le azioni appropriate.

   Questo evento supera l&#39;avviso appropriato. L’applicazione determina come procedere, ad esempio, provando di nuovo la ricerca o continuando la riproduzione dalla posizione precedente.

1. Attendi che TVSDK chiami il callback `QOSEventListener.onSeekComplete`.
1. Recuperate la posizione di riproduzione rettificata finale utilizzando il parametro di posizione del callback.

   Questo è importante perché la posizione iniziale effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Il comportamento di riproduzione potrebbe essere interessato se una ricerca o un altro riposizionamento termina al centro di un&#39;interruzione di annuncio o salta le interruzioni di annuncio.

1. Utilizzate le informazioni sulla posizione quando visualizzate una barra di scorrimento della ricerca.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Esempio di ricerca**

In questo esempio, l&#39;utente scorre la barra di ricerca per cercare la posizione desiderata.

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

