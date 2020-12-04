---
description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-title: Caricamento di una risorsa multimediale in MediaPlayer
title: Caricamento di una risorsa multimediale in MediaPlayer
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 4ef05be045334a2e723da4c7c6a7ee22fb0f776c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Caricare una risorsa multimediale in MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Caricate una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Imposta l’elemento riproducibile di MediaPlayer con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento attualmente riproducibile di MediaPlayer esistente chiamando `MediaPlayer.replaceCurrentItem` e passando un&#39;istanza `MediaResource` esistente.

1. Registra un&#39;implementazione dell&#39;interfaccia `MediaPlayer.PlaybackEventListener` con l&#39;istanza `MediaPlayer`.

   * `onPrepared`
   * `onStateChanged`, e controllare se sono INITIALIZZATI e ERRORE.

1. Quando lo stato del lettore multimediale diventa INITIALIZED, è possibile chiamare `MediaPlayer.prepareToPlay`

   Lo stato INITIALIZED indica che il supporto è stato caricato correttamente. La chiamata di `prepareToPlay` avvia la risoluzione e il processo di posizionamento della pubblicità, se presente.

1. Quando TVSDK chiama il callback `onPrepared`, il flusso multimediale è stato caricato correttamente ed è pronto per la riproduzione.

   Quando viene caricato il flusso multimediale, viene creato un `MediaPlayerItem`.

>Se si verifica un errore, lo stato `MediaPlayer` viene cambiato in ERROR. Inoltre, invia una notifica all&#39;applicazione chiamando il callback `PlaybackEventListener.onStateChanged`.
>
>Questo passa diversi parametri:
>* Un parametro `state` di tipo `MediaPlayer.PlayerState` con il valore di `MediaPlayer.PlayerState.ERROR`.
   >
   >
* Un parametro `notification` di tipo `MediaPlayerNotification` che contiene informazioni diagnostiche sull&#39;evento di errore.


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
