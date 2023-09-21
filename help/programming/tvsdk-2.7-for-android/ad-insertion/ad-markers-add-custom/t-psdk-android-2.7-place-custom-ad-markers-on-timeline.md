---
description: Questo esempio mostra il modo consigliato per includere marcatori annuncio personalizzati nella timeline di riproduzione.
title: Posizionare marcatori annuncio personalizzati sulla timeline
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Posizionare marcatori annuncio personalizzati sulla timeline {#place-custom-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato per includere marcatori annuncio personalizzati nella timeline di riproduzione.

1. Tradurre le informazioni sul posizionamento degli annunci fuori banda in un elenco o array di `RepaceTimeRange` classe.
1. Crea un&#39;istanza di `CustomRangeMetadata` e utilizza i relativi `setTimeRangeList` metodo con list/array come argomento per impostare l&#39;elenco dell&#39;intervallo di tempo.
1. Utilizza i suoi `setType` metodo per impostare il tipo su `MARK_RANGE`.
1. Utilizza il `MediaPlayerItemConfig.setCustomRangeMetadata` metodo con `CustomRangeMetadata` come argomento per impostare i metadati dell’intervallo personalizzato.
1. Utilizza il `MediaPlayer.replaceCurrentResource` metodo con `MediaPlayerItemConfig` come argomento da impostare, imposta la nuova risorsa come risorsa corrente.
1. Attendi un `STATE_CHANGED` , che segnala che il lettore si trova nel `PREPARED` stato.
1. Avvia riproduzione video chiamando `MediaPlayer.play`.

Ecco il risultato del completamento delle attività in questo esempio: >
* Se un `ReplaceTimeRange` si sovrappone a un altro nella timeline di riproduzione, ad esempio, la posizione iniziale di un `ReplaceTimeRange` è precedente a una posizione finale già posizionata, TVSDK regola automaticamente l’inizio dell’offesa `ReplaceTimeRange` per evitare il conflitto.

  In questo modo le `ReplaceTimeRange` più breve di quello specificato in origine. Se la regolazione porta a una durata pari a zero, TVSDK rilascia silenziosamente l’offensiva `ReplaceTimeRange`.

* TVSDK cerca intervalli di tempo adiacenti per le interruzioni pubblicitarie personalizzate e li raggruppa in interruzioni pubblicitarie separate.

  Gli intervalli di tempo non adiacenti a nessun altro intervallo di tempo vengono convertiti in interruzioni pubblicitarie che contengono un singolo annuncio.
* Se l’applicazione tenta di caricare una risorsa multimediale la cui configurazione contiene `CustomRangeMetadata` che può essere utilizzato solo nei marcatori di annunci personalizzati contestuali, TVSDK genera un’eccezione se la risorsa sottostante non è di tipo VOD.
* Quando si tratta di marcatori di annunci personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (ad esempio, Adobe Primetime ad decisioning).

  Puoi utilizzare qualsiasi modulo TVSDK ad-resolver o il meccanismo personalizzato per i marcatori degli annunci. Quando utilizzi marcatori annuncio personalizzati, il contenuto dell’annuncio viene considerato risolto e posizionato sulla timeline.

Il seguente frammento di codice inserisce tre intervalli di tempo sulla timeline come marcatori di annunci personalizzati.

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
