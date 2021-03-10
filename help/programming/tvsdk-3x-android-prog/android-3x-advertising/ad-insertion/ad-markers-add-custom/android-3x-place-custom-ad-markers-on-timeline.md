---
description: Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.
title: Posizionare marcatori di annunci personalizzati sulla timeline
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Posiziona marcatori di annunci personalizzati sulla timeline {#place-custom-ad-markers-on-the-timeline}

Questo esempio mostra il modo consigliato di includere indicatori di annunci personalizzati nella timeline di riproduzione.

1. Traduci le informazioni di posizionamento degli annunci fuori banda in un elenco/array di `RepaceTimeRange` classe.
1. Creare un&#39;istanza della classe `CustomRangeMetadata` e utilizzare il relativo metodo `setTimeRangeList` con l&#39;elenco/array come argomento per impostare l&#39;elenco di intervalli di tempo.
1. Utilizzare il metodo `setType` per impostare il tipo su `MARK_RANGE`.
1. Utilizza il metodo `MediaPlayerItemConfig.setCustomRangeMetadata` con l&#39;istanza `CustomRangeMetadata` come argomento per impostare i metadati dell&#39;intervallo personalizzati.
1. Utilizza il metodo `MediaPlayer.replaceCurrentResource` con l’istanza `MediaPlayerItemConfig` come argomento per impostare la nuova risorsa come corrente.
1. Attendi un evento `STATE_CHANGED` che segnala che il lettore è nello stato `PREPARED`.
1. Avvia la riproduzione video chiamando `MediaPlayer.play`.

Di seguito è riportato il risultato del completamento delle attività in questo esempio:

* Se un elemento `ReplaceTimeRange` si sovrappone a un altro nella timeline di riproduzione, ad esempio, la posizione iniziale di un elemento `ReplaceTimeRange` è precedente a una posizione finale già inserita, TVSDK regola automaticamente l&#39;inizio dell&#39; elemento `ReplaceTimeRange` offensivo per evitare il conflitto.

   Questo rende il `ReplaceTimeRange` corretto più breve di quanto specificato originariamente. Se la regolazione porta a una durata pari a zero, TVSDK rilascia silenziosamente il `ReplaceTimeRange` dannoso.

* TVSDK cerca intervalli di tempo adiacenti per le interruzioni di annunci personalizzate e le raggruppa in interruzioni di annunci separate.

Gli intervalli di tempo non adiacenti a qualsiasi altro intervallo di tempo vengono convertiti in interruzioni di annunci che contengono un singolo annuncio.

* Se l’applicazione tenta di caricare una risorsa multimediale la cui configurazione contiene `CustomRangeMetadata` che può essere utilizzata solo nei marcatori di annunci personalizzati del contesto, TVSDK genera un’eccezione se la risorsa sottostante non è di tipo VOD.

* Quando si tratta di ad markers personalizzati, TVSDK disattiva altri meccanismi di risoluzione degli annunci (ad esempio, Adobe Primetime ad Decioning).

   Puoi utilizzare qualsiasi modulo ad-resolver TVSDK o il meccanismo di ad markers personalizzato. Quando utilizzi marcatori di annunci personalizzati, il contenuto dell’annuncio viene considerato risolto e posizionato sulla timeline.

Lo snippet di codice seguente inserisce tre intervalli di tempo sulla timeline come marcatori di annunci personalizzati.

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
