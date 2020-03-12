---
description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-title: Caricamento di una risorsa multimediale in MediaPlayer
title: Caricamento di una risorsa multimediale in MediaPlayer
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Caricamento di una risorsa multimediale in MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Caricate una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Impostare l&#39;elemento `MediaPlayer` riproducibile dell&#39;oggetto con la nuova risorsa da riprodurre.

   Sostituisci l’elemento attualmente riproducibile di MediaPlayer esistente chiamando `MediaPlayer.replaceCurrentResource` e passando un’ `MediaResource` istanza esistente.

1. Verificare almeno le seguenti modifiche:

   * INIZIALIZZATO
   * PREPARATO
   * ERRORE

      Attraverso questi eventi, l&#39; `MediaPlayer` oggetto può inviare una notifica all&#39;applicazione quando la risorsa multimediale viene caricata correttamente.

1. Quando lo stato del lettore multimediale diventa INITIALIZED, potete chiamare `MediaPlayer.prepareToPlay`

   Lo stato INITIALIZED indica che il supporto è stato caricato correttamente. La chiamata `prepareToPlay` avvia il processo di risoluzione e posizionamento pubblicitario, se presente.

1. Quando lo stato del lettore multimediale cambia in PREPARATO, il flusso multimediale è stato caricato correttamente ed è pronto per la riproduzione.

   Quando il flusso multimediale viene caricato, `MediaPlayerItem` viene creato un

Se si verifica un errore, MediaPlayer passa allo stato ERROR. Invia inoltre una notifica all’applicazione inviando l’ `STATUS_CHANGED` evento al `MediaPlayerStatusChangeEvent` callback.

Questo passa diversi parametri: >
* Un `type` parametro di tipo stringa con il valore `ERROR`.

* Un `MediaError` parametro che può essere utilizzato per ottenere una notifica contenente informazioni diagnostiche sull&#39;evento di errore.


><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


Il seguente codice di esempio semplificato illustra il processo di caricamento di una risorsa multimediale:
>```>
>>// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                            onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
  switch(event.status) { 
     case MediaPlayerStatus.INITIALIZED: 
         // at this point, the resource is successfully loaded 
         // the media player will provide a reference to the current 
         // "playable item" ( is guarantee to be valid and not-null). 
         var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
         // we can take a look at the media item characteristics like 
         // alternate audio tracks, profile information, if is a live stream 
         // if is drm protected 
         mediaPlayer.prepareToPlay(); 
         break; 
   case MediaPlayerStatus.PREPARED: 
        // at this point, the resource is successfully processed all  
        // advertisement placements have been executed and the the  
        // MediaPlayer is ready to start the playback 
       if (autoPlay) { 
           mediaPlayer.play(); 
       } 
       break; 
   case MediaPlayerStatus.ERROR: 
       // something bad happened - the resource cannot be loaded 
       // details about the problem are provided via the event.error property 
       break; 
       // implementation of the other methods in the PlaybackEventListener interface 
       ... 
   } 
}
```>
>
