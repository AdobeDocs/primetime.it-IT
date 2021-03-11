---
description: Carica una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è un modo per caricare una risorsa multimediale.
title: Caricare una risorsa multimediale in MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Carica una risorsa multimediale in MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Carica una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è un modo per caricare una risorsa multimediale.

1. Imposta l&#39;elemento riproducibile dell&#39;oggetto `MediaPlayer` con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento attualmente riproducibile di MediaPlayer chiamando `MediaPlayer.replaceCurrentResource` e passando un&#39;istanza `MediaResource` esistente.

1. Verifica almeno le seguenti modifiche:

   * INIZIALIZZATO
   * PREPARATO
   * ERRORE

      Attraverso questi eventi, l&#39;oggetto `MediaPlayer` può inviare una notifica all&#39;applicazione quando la risorsa multimediale viene caricata correttamente.

1. Quando lo stato del lettore multimediale diventa INITIALIZED, puoi chiamare `MediaPlayer.prepareToPlay`

   Lo stato INITIALIZED indica che il supporto è stato caricato correttamente. Una chiamata a `prepareToPlay` avvia il processo di risoluzione e posizionamento dei messaggi pubblicitari, se presente.

1. Quando lo stato del lettore multimediale cambia in PREPARED, il flusso multimediale è stato caricato correttamente ed è pronto per la riproduzione.

   Quando il flusso multimediale viene caricato, viene creato un `MediaPlayerItem`.

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
