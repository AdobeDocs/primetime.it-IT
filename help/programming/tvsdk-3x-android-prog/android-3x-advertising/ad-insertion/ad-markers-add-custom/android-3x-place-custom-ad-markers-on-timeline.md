---
description: Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.
seo-description: Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.
seo-title: Inserisci indicatori di annunci personalizzati nella timeline
title: Inserisci indicatori di annunci personalizzati nella timeline
uuid: 47e31a97-e5da-46f3-bdcc-327c159c4355
translation-type: tm+mt
source-git-commit: 2a6ea34968ee7085931f99a24dfb23d097721b89
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Posiziona indicatori di annunci personalizzati sulla timeline {#place-custom-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.

1. Traducete le informazioni di posizionamento degli annunci fuori banda in un elenco/array di `RepaceTimeRange` classe.
1. Create un&#39;istanza della classe `CustomRangeMetadata` e utilizzate il relativo metodo `setTimeRangeList` con l&#39;argomento list/array per impostare l&#39;elenco dei relativi intervalli di tempo.
1. Utilizzare il metodo `setType` per impostare il tipo su `MARK_RANGE`.
1. Utilizzate il metodo `MediaPlayerItemConfig.setCustomRangeMetadata` con l&#39;istanza `CustomRangeMetadata` come argomento per impostare i metadati dell&#39;intervallo personalizzato.
1. Utilizzare il metodo `MediaPlayer.replaceCurrentResource` con l&#39;istanza `MediaPlayerItemConfig` come argomento per impostare la nuova risorsa come quella corrente.
1. Attendete un evento `STATE_CHANGED` che indichi che il lettore è nello stato `PREPARED`.
1. Avviate la riproduzione video chiamando `MediaPlayer.play`.

Questo è il risultato del completamento delle attività in questo esempio:

* Se un elemento `ReplaceTimeRange` si sovrappone a un altro nella timeline di riproduzione, ad esempio, la posizione iniziale di un elemento `ReplaceTimeRange` è precedente a una posizione finale già inserita, TVSDK regola automaticamente l&#39;inizio dell&#39;elemento `ReplaceTimeRange` offensivo per evitare il conflitto.

   Questo rende il `ReplaceTimeRange` corretto più breve di quanto specificato originariamente. Se la regolazione porta a una durata pari a zero, TVSDK elimina in modo invisibile l&#39;elemento `ReplaceTimeRange` offensivo.

* TVSDK cerca intervalli di tempo adiacenti per interruzioni di annunci personalizzate e li raggruppa in interruzioni di annunci separate.

Gli intervalli di tempo non adiacenti a qualsiasi altro intervallo di tempo vengono convertiti in interruzioni di annunci contenenti un singolo annuncio.

* Se l’applicazione tenta di caricare una risorsa multimediale la cui configurazione contiene `CustomRangeMetadata` che può essere utilizzata solo nei marcatori di annunci personalizzati del contesto, TVSDK genera un’eccezione se la risorsa sottostante non è di tipo VOD.

* Quando si tratta di indicatori di annunci personalizzati, TVSDK disattiva altri meccanismi di risoluzione di annunci (ad esempio,  il processo decisionale di Adobe Primetime).

   Puoi utilizzare qualsiasi modulo di risoluzione di annunci TVSDK o il meccanismo di marketing degli annunci personalizzato. Quando utilizzate marcatori pubblicitari personalizzati, il contenuto dell&#39;annuncio viene considerato risolto e viene inserito nella timeline.

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
