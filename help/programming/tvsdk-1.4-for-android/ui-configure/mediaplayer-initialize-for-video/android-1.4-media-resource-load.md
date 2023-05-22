---
description: Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
title: Caricare una risorsa multimediale in MediaPlayer
exl-id: 2d5e95bc-3962-4356-b90f-e550066f7a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Caricare una risorsa multimediale in MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Imposta l&#39;elemento riproducibile del lettore multimediale con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento attualmente riproducibile del lettore multimediale esistente chiamando `MediaPlayer.replaceCurrentItem` e il passaggio di un `MediaResource` dell&#39;istanza.

1. Registra un&#39;implementazione di `MediaPlayer.PlaybackEventListener` interfaccia con `MediaPlayer` dell&#39;istanza.

   * `onPrepared`
   * `onStateChanged`, e verificare se sono stati impostati i valori INITIALIZED ed ERROR.

1. Quando lo stato del lettore multimediale diventa INITIALIZED, è possibile chiamare `MediaPlayer.prepareToPlay`

   Lo stato INIZIALIZZATO indica che il supporto è stato caricato correttamente. Chiamata `prepareToPlay` avvia il processo di risoluzione e posizionamento pubblicitario, se presente.

1. Quando TVSDK chiama `onPrepared` callback, il flusso multimediale è stato caricato correttamente ed è pronto per la riproduzione.

   Quando il flusso multimediale viene caricato, `MediaPlayerItem` viene creato.

>Se si verifica un errore, il `MediaPlayer` passa allo stato ERROR. Notifica inoltre l&#39;applicazione chiamando il `PlaybackEventListener.onStateChanged`callback.
>
>In questo modo vengono trasmessi diversi parametri:
>* A `state` parametro di tipo `MediaPlayer.PlayerState` con il valore di `MediaPlayer.PlayerState.ERROR`.
>
>* A `notification` parametro di tipo `MediaPlayerNotification` che contiene informazioni di diagnostica sull’evento di errore.


Il seguente codice di esempio semplificato illustra il processo di caricamento di una risorsa multimediale:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```
