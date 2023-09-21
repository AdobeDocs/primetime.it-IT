---
description: Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.
title: Posizionare i marcatori degli annunci TimeRange sulla timeline
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Posizionare i marcatori degli annunci TimeRange sulla timeline {#place-timerange-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.

1. Tradurre le informazioni sul posizionamento degli annunci fuori banda in un elenco di `TimeRange` specifiche (ovvero istanze del `TimeRange` classe).
1. Utilizza il set di `TimeRange` specifiche per compilare un&#39;istanza del `TimeRangeCollection` classe.
1. Passa l’istanza di metadati, che può essere ottenuta da `TimeRangeCollection` istanza, al `replaceCurrentItem` (parte dell&#39;interfaccia MediaPlayer).
1. Attendi la transizione di TVSDK a `PREPARED` attendendo il `PlaybackEventListener#onPrepared` callback da attivare.
1. Avvia la riproduzione del video chiamando il `play()` metodo (parte del metodo `MediaPlayer` ).

* Gestione dei conflitti della timeline: in alcuni casi `TimeRange` le specifiche si sovrappongono sulla timeline di riproduzione. Ad esempio, il valore della posizione iniziale corrispondente a `TimeRange` la specifica potrebbe essere inferiore al valore della posizione finale già posizionata. In questo caso, TVSDK regola automaticamente la posizione iniziale dell&#39;offesa `TimeRange` specifica per evitare conflitti nella timeline. Grazie a questa regolazione, il nuovo `TimeRange` diventa più breve di quanto originariamente specificato. Se l&#39;aggiustamento è così estremo da portare ad una `TimeRange` con una durata di zero ms, TVSDK rilascia silenziosamente l’offensiva `TimeRange` specifica.
* Quando `TimeRange` specifiche per le interruzioni pubblicitarie personalizzate, TVSDK tenta di tradurle in annunci raggruppati all’interno di interruzioni pubblicitarie. TVSDK cerca adiacenti `TimeRange` e li raggruppa in interruzioni pubblicitarie separate. Se esistono intervalli di tempo non adiacenti a nessun altro intervallo di tempo, vengono convertiti in interruzioni pubblicitarie che contengono un singolo annuncio.
* Si presume che l’elemento del lettore multimediale che viene caricato punti a una risorsa VOD. TVSDK controlla questo valore ogni volta che l’applicazione tenta di caricare una risorsa multimediale i cui metadati contengono `TimeRange` specifiche che possono essere utilizzate solo nel contesto della funzione marcatori annuncio personalizzati. Se la risorsa sottostante non è di tipo VOD, la libreria TVSDK genera un’eccezione.
* Quando si tratta di marcatori di annunci personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (tramite Adobe Primetime ad decisioning (precedentemente noto come Auditude) o altro sistema di provisioning di annunci). Puoi utilizzare uno dei vari moduli ad-resolver forniti da TVSDK o il meccanismo personalizzato per i marcatori degli annunci. Quando utilizzi l’API per i marcatori di annunci personalizzati, il contenuto dell’annuncio viene considerato già risolto e inserito nella timeline.

Il seguente snippet di codice fornisce un semplice esempio in cui un set di tre specifiche TimeRange viene inserito sulla timeline come marcatori annuncio personalizzati.

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
