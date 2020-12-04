---
description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-title: Caricamento di una risorsa multimediale in MediaPlayer
title: Caricamento di una risorsa multimediale in MediaPlayer
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: 84924d84bfa436a8807c2e8d74d1dc268d457051
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# Carica una risorsa multimediale in MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Caricate una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Impostate l&#39;elemento riproducibile dell&#39;oggetto `MediaPlayer` con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento attualmente riproducibile di MediaPlayer esistente chiamando `MediaPlayer.replaceCurrentResource` e passando un&#39;istanza `MediaResource` esistente.

1. Verificare almeno le seguenti modifiche:

   * INIZIALIZZATO
   * PREPARATO
   * ERRORE

      Attraverso questi eventi, l&#39;oggetto `MediaPlayer` può inviare una notifica all&#39;applicazione quando la risorsa multimediale viene caricata correttamente.

1. Quando lo stato del lettore multimediale diventa INITIALIZED, è possibile chiamare `MediaPlayer.prepareToPlay`

   Lo stato INITIALIZED indica che il supporto è stato caricato correttamente. La chiamata di `prepareToPlay` avvia la risoluzione e il processo di posizionamento della pubblicità, se presente.

1. Quando lo stato del lettore multimediale cambia in PREPARATO, il flusso multimediale è stato caricato correttamente ed è pronto per la riproduzione.

   Quando viene caricato il flusso multimediale, viene creato un `MediaPlayerItem`.

Se si verifica un errore, MediaPlayer passa allo stato ERROR. Invia inoltre una notifica all&#39;applicazione inviando l&#39;evento `STATUS_CHANGED` al callback `MediaPlayerStatusChangeEvent`.

Questo passa diversi parametri:
* Un parametro `type` di tipo stringa con il valore `ERROR`.

* Un parametro `MediaError` che può essere utilizzato per ottenere una notifica contenente informazioni diagnostiche sull&#39;evento di errore.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

Il seguente codice di esempio semplificato illustra il processo di caricamento di una risorsa multimediale:

```
// mediaResource is a properly configured MediaResource instance 
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
```
