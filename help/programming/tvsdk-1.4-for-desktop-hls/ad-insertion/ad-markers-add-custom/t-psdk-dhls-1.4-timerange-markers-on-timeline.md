---
description: Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.
seo-description: Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.
seo-title: Inserite i marcatori TimeRange nella timeline
title: Inserite i marcatori TimeRange nella timeline
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: fd21a29bb186238142d43e0277bbf92f8406f6f7
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Posizionare i marcatori TimeRange sulla timeline {#place-timerange-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato per includere le specifiche TimeRange nella timeline di riproduzione.

1. Tradurre le informazioni di posizionamento degli annunci fuori banda in un elenco di `TimeRange` specifiche (ovvero, istanze della classe `TimeRange`).
1. Utilizzare il set di specifiche `TimeRange` per compilare un&#39;istanza della classe `TimeRangeCollection`.
1. Passa l&#39;istanza Metadata, che può essere ottenuta dall&#39;istanza `TimeRangeCollection`, al metodo `replaceCurrentItem` (parte dell&#39;interfaccia `MediaPlayer`).
1. Attendete che TVSDK passi allo stato PREPARATO in attesa che venga attivato il callback `PlaybackEventListener#onPrepared`.
1. Avviare la riproduzione video chiamando il metodo `play()` (parte dell&#39;interfaccia `MediaPlayer`).

* Gestione dei conflitti della timeline: Potrebbero verificarsi casi in cui alcune specifiche `TimeRange` si sovrappongono sulla timeline di riproduzione. Ad esempio, il valore della posizione iniziale corrispondente a una specifica `TimeRange` potrebbe essere inferiore al valore della posizione finale già inserita. In questo caso, TVSDK regola in modo invisibile la posizione iniziale della specifica `TimeRange` offensiva per evitare conflitti con la cronologia. Grazie a questa regolazione, la nuova `TimeRange` diventa più breve di quanto specificato originariamente. Se la regolazione è così estrema che porta a un valore `TimeRange` con una durata di zero ms, TVSDK elimina in modo invisibile la specifica `TimeRange` che si ritiene offensiva.

* Quando vengono fornite le specifiche `TimeRange` per le interruzioni pubblicitarie personalizzate, TVSDK tenta di tradurle in annunci raggruppati all&#39;interno di interruzioni pubblicitarie. TVSDK cerca specifiche `TimeRange` adiacenti e le raggruppa in interruzioni pubblicitarie separate. Se sono presenti intervalli di tempo non adiacenti ad altri intervalli, questi vengono convertiti in interruzioni pubblicitarie contenenti un singolo annuncio.

* Si presume che l’elemento del lettore multimediale che viene caricato punti a una risorsa VOD. TVSDK verifica questo problema ogni volta che l&#39;applicazione tenta di caricare una risorsa multimediale i cui metadati contengono specifiche `TimeRange` che possono essere utilizzate solo nel contesto della funzione di annunci pubblicitari personalizzati. Se la risorsa sottostante non è di tipo VOD, la libreria TVSDK genera un&#39;eccezione.

* Quando si tratta di annunci pubblicitari personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (tramite  Adobe Primetime ad Decision (precedentemente noto come Auditude) o altri sistemi di provisioning degli annunci). Potete utilizzare uno dei vari moduli per la risoluzione di annunci forniti da TVSDK o il meccanismo di marcatori di annunci personalizzati. Quando si utilizza l&#39;API per marcatori pubblicitari personalizzati, il contenuto dell&#39;annuncio viene considerato già risolto e inserito nella timeline.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

Il frammento di codice seguente fornisce un esempio semplice in cui un set di tre `TimeRange` specifiche viene inserito nella timeline come indicatori pubblicitari personalizzati.

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
