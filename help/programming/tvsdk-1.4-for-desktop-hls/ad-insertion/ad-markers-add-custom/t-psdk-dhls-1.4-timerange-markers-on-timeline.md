---
description: Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.
title: Posizionare i marcatori di annunci TimeRange sulla timeline
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Posizionare i marcatori di annunci TimeRange sulla timeline {#place-timerange-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.

1. Traduci le informazioni di posizionamento degli annunci fuori banda in un elenco di `TimeRange` specifiche (ovvero, istanze della classe `TimeRange`).
1. Utilizza l&#39;insieme di specifiche `TimeRange` per popolare un&#39;istanza della classe `TimeRangeCollection`.
1. Passa l’istanza Metadati , che può essere ottenuta dall’istanza `TimeRangeCollection`, al metodo `replaceCurrentItem` (parte dell’interfaccia `MediaPlayer`).
1. Attendi che TVSDK passi alla transizione allo stato PREPARATO in attesa che venga attivato il callback `PlaybackEventListener#onPrepared` .
1. Avvia la riproduzione video chiamando il metodo `play()` (parte dell&#39;interfaccia `MediaPlayer`).

* Gestione dei conflitti della timeline: Ci possono essere casi in cui alcune specifiche `TimeRange` si sovrappongono sulla timeline di riproduzione. Ad esempio, il valore della posizione iniziale corrispondente a una specifica `TimeRange` potrebbe essere inferiore al valore della posizione finale già inserita. In questo caso, TVSDK regola in modo invisibile la posizione iniziale della specifica `TimeRange` offesa per evitare conflitti nella timeline. Grazie a questa regolazione, il nuovo `TimeRange` diventa più breve di quanto specificato originariamente. Se la regolazione è così estrema che porterebbe a un `TimeRange` con una durata di zero ms, TVSDK rilascia silenziosamente la specifica `TimeRange` che causa il danno.

* Quando vengono fornite le specifiche `TimeRange` per le interruzioni di annunci personalizzate, TVSDK tenta di tradurle in annunci raggruppati all’interno di interruzioni di annunci. TVSDK cerca le specifiche adiacenti `TimeRange` e le raggruppa in interruzioni pubblicitarie separate. Se ci sono intervalli di tempo che non sono adiacenti a nessun altro intervallo di tempo, vengono tradotti in interruzioni pubblicitarie che contengono un singolo annuncio.

* Si presume che l&#39;elemento del lettore multimediale caricato punti a una risorsa VOD. TVSDK lo controlla ogni volta che l’applicazione prova a caricare una risorsa multimediale i cui metadati contengono `TimeRange` specifiche che possono essere utilizzate solo nel contesto della funzione di ad-markers personalizzata. Se la risorsa sottostante non è di tipo VOD, la libreria TVSDK genera un&#39;eccezione.

* Quando si utilizzano marcatori di annunci personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (tramite Adobe Primetime ad Decioning (precedentemente noto come Auditude) o altri sistemi di provisioning degli annunci). Puoi utilizzare uno dei vari moduli ad-resolver forniti da TVSDK o il meccanismo di ad-markers personalizzato. Quando si utilizza l’API degli ad-markers personalizzata, il contenuto dell’annuncio viene considerato già risolto e inserito nella timeline.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

Il seguente frammento di codice fornisce un semplice esempio in cui un set di tre `TimeRange` specifiche viene inserito sulla timeline come ad-markers personalizzati.

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
