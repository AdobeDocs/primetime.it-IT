---
description: Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
title: Caricare una risorsa multimediale in MediaPlayer
exl-id: 8258c45e-f8bf-434d-9621-88c189e1530d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Caricare una risorsa multimediale in MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Imposta il `MediaPlayer` elemento riproducibile dell’oggetto con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento attualmente riproducibile del lettore multimediale esistente chiamando `MediaPlayer.replaceCurrentResource` e il passaggio di un `MediaResource` dell&#39;istanza.

1. Verifica almeno le seguenti modifiche:

   * INIZIALIZZATO
   * PREPARATO
   * ERRORE

      Attraverso questi eventi, il `MediaPlayer` L&#39;oggetto può notificare l&#39;applicazione quando la risorsa multimediale viene caricata correttamente.

1. Quando lo stato del lettore multimediale diventa INITIALIZED, è possibile chiamare `MediaPlayer.prepareToPlay`

   Lo stato INIZIALIZZATO indica che il supporto è stato caricato correttamente. Chiamata `prepareToPlay` avvia il processo di risoluzione e posizionamento pubblicitario, se presente.

1. Quando lo stato del lettore multimediale cambia in PREPARATO, il flusso multimediale è stato caricato correttamente ed è pronto per la riproduzione.

   Quando il flusso multimediale viene caricato, `MediaPlayerItem` viene creato.

In caso di errore, MediaPlayer passa allo stato ERROR. Notifica inoltre l’applicazione inviando `STATUS_CHANGED` evento al tuo `MediaPlayerStatusChangeEvent` callback.

In questo modo vengono trasmessi diversi parametri:
* A `type` parametro di tipo stringa con valore `ERROR`.

* A `MediaError` parametro che è possibile utilizzare per ottenere una notifica contenente informazioni di diagnostica sull&#39;evento di errore.


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
