---
description: Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.
seo-description: Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.
seo-title: Inserisci indicatori di annunci personalizzati nella timeline
title: Inserisci indicatori di annunci personalizzati nella timeline
uuid: ee74d1f3-7186-44b8-bad7-55af579842e8
translation-type: tm+mt
source-git-commit: 9f1f27bc6c23994338775a32f978a2e768a0f3aa

---


# Inserisci indicatori di annunci personalizzati nella timeline {#place-custom-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.

1. Tradurre le informazioni di posizionamento degli annunci fuori banda in un elenco o array di `RepaceTimeRange` classi.
1. Creare un&#39;istanza di `CustomRangeMetadata` classe e utilizzare il relativo `setTimeRangeList` metodo con l&#39;argomento list/array per impostare l&#39;elenco dei relativi intervalli di tempo.
1. Utilizzate il relativo `setType` metodo per impostare il tipo su `MARK_RANGE`.
1. Usate il `MediaPlayerItemConfig.setCustomRangeMetadata` metodo con l’ `CustomRangeMetadata` istanza come argomento per impostare i metadati dell’intervallo personalizzato.
1. Utilizzare il `MediaPlayer.replaceCurrentResource` metodo con l&#39; `MediaPlayerItemConfig` istanza come argomento per impostare la nuova risorsa come quella corrente.
1. Attendi un `STATE_CHANGED` evento, che segnala che il lettore è nello `PREPARED` stato.
1. Avviate la riproduzione del video chiamando `MediaPlayer.play`.

Questo è il risultato del completamento delle attività in questo esempio: >
* Se un `ReplaceTimeRange` elemento si sovrappone a un altro nella timeline di riproduzione, ad esempio, la posizione iniziale di un `ReplaceTimeRange` elemento è precedente a una posizione finale già inserita, TVSDK regola automaticamente l’inizio dell’offeso `ReplaceTimeRange` per evitare il conflitto.

   Questo rende la correzione `ReplaceTimeRange` più breve di quanto specificato originariamente. Se la regolazione porta a una durata pari a zero, TVSDK elimina in modo invisibile l’offeso `ReplaceTimeRange`.

* TVSDK cerca intervalli di tempo adiacenti per interruzioni di annunci personalizzate e li raggruppa in interruzioni di annunci separate.

   Gli intervalli di tempo non adiacenti a qualsiasi altro intervallo di tempo vengono convertiti in interruzioni di annunci contenenti un singolo annuncio.
* Se l’applicazione tenta di caricare una risorsa multimediale la cui configurazione contiene `CustomRangeMetadata` che può essere utilizzata solo negli indicatori di annunci personalizzati del contesto, TVSDK genera un’eccezione se la risorsa sottostante non è di tipo VOD.
* Quando lavorate con gli indicatori di annunci personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (ad esempio, il processo di decisione degli annunci Adobe Primetime).

   Puoi utilizzare qualsiasi modulo di risoluzione di annunci TVSDK o il meccanismo di marketing per annunci personalizzati. Quando utilizzate marcatori pubblicitari personalizzati, il contenuto dell&#39;annuncio viene considerato risolto e viene inserito nella timeline.

Il frammento di codice seguente inserisce tre intervalli di tempo sulla timeline come indicatori di annunci personalizzati.

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
