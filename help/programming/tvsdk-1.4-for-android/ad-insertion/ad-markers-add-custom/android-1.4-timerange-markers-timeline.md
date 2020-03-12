---
description: Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.
seo-description: Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.
seo-title: Inserite i marcatori TimeRange nella timeline
title: Inserite i marcatori TimeRange nella timeline
uuid: 12935eba-2e91-40ea-a60e-02d0060c3cce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inserite i marcatori TimeRange nella timeline {#place-timerange-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.

1. Tradurre le informazioni di posizionamento degli annunci fuori banda in un elenco di `TimeRange` specifiche (ovvero, istanze della `TimeRange` classe).
1. Utilizzare il set di `TimeRange` specifiche per compilare un&#39;istanza della `TimeRangeCollection` classe.
1. Passate l’istanza Metadata, che può essere ottenuta dall’ `TimeRangeCollection` istanza, al `replaceCurrentItem` metodo (parte dell’interfaccia di MediaPlayer).
1. Attendete che TVSDK passi allo `PREPARED` stato in attesa dell&#39;attivazione del `PlaybackEventListener#onPrepared` callback.
1. Avviate la riproduzione video chiamando il `play()` metodo (parte dell’ `MediaPlayer` interfaccia).

* Gestione dei conflitti della timeline: Potrebbero verificarsi casi in cui alcune `TimeRange` specifiche si sovrappongono sulla timeline di riproduzione. Ad esempio, il valore della posizione iniziale corrispondente a una `TimeRange` specifica potrebbe essere inferiore al valore della posizione finale già inserita. In questo caso, TVSDK regola in modo invisibile la posizione iniziale della `TimeRange` specifica offendente per evitare conflitti nella cronologia. Grazie a questa regolazione, il nuovo `TimeRange` diventa più corto di quanto originariamente specificato. Se la regolazione è così estrema che potrebbe portare a un valore `TimeRange` con una durata di zero ms, TVSDK elimina in modo invisibile la `TimeRange` specifica indesiderata.
* Quando vengono fornite `TimeRange` le specifiche per le interruzioni di annunci personalizzate, TVSDK tenta di tradurle in annunci raggruppati all&#39;interno di interruzioni di annunci. TVSDK cerca `TimeRange` specifiche adiacenti e le raggruppa in interruzioni pubblicitarie separate. Se sono presenti intervalli di tempo non adiacenti ad altri intervalli, vengono convertiti in interruzioni pubblicitarie contenenti un singolo annuncio.
* Si presume che l’elemento del lettore multimediale che viene caricato punti a una risorsa VOD. TVSDK verifica questo problema ogni volta che l’applicazione tenta di caricare una risorsa multimediale i cui metadati contengono `TimeRange` specifiche che possono essere utilizzate solo nel contesto della funzione di annunci pubblicitari personalizzati. Se la risorsa sottostante non è di tipo VOD, la libreria TVSDK genera un&#39;eccezione.
* Quando si tratta di annunci pubblicitari personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (tramite il processo di decisione degli annunci Adobe Primetime (precedentemente noto come Auditude) o altri sistemi di provisioning degli annunci). Potete utilizzare uno dei vari moduli per la risoluzione di annunci forniti da TVSDK o il meccanismo di marcatori di annunci personalizzati. Quando si utilizza l&#39;API per marcatori pubblicitari personalizzati, il contenuto dell&#39;annuncio viene considerato già risolto e inserito nella timeline.

Il frammento di codice seguente fornisce un esempio semplice in cui un set di tre specifiche TimeRange viene inserito nella timeline come indicatori di annunci personalizzati.

```java>
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
TimeRangeCollection timeRanges = new TimeRangeCollection();  
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
 
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                               timeRanges.toMetadata(null)); 
 
// prepare the content for playback by creating 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentItem(mediaResource); 
// wait for TVSDK to reach the PREPARED state 
... 
MediaPlayer.PlaybackEventListener playbackEventListener = new 
  MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // TVSDK in in the PREPARED state. We are allowed to start the playback  
        mediaPlayer.play(); 
    } 
} 
```
