---
description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
seo-title: Caricare una risorsa multimediale nel lettore multimediale
title: Caricare una risorsa multimediale nel lettore multimediale
uuid: 0334fa69-1d92-44d8-8891-2bc90a1ea498
translation-type: tm+mt
source-git-commit: 67975894814fbed8cfc49764a54b80d123032a49

---


# Caricare una risorsa multimediale nel lettore multimediale {#load-a-media-resource-in-the-media-player}

Caricate una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Impostare il lettore multimediale per riprodurre la nuova risorsa.

   Sostituisce l’elemento attualmente riproducibile chiamando `MediaPlayer.replaceCurrentResource()` e passando un’ `MediaResource` istanza esistente.

   Viene avviato il processo di caricamento delle risorse.

1. Registra l’ `MediaPlayerEvent.STATUS_CHANGED` evento con l’ `MediaPlayer` istanza. Nella callback, verificate che siano presenti almeno i seguenti valori di stato:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`
   Attraverso questi eventi, l&#39; `MediaPlayer` oggetto notifica all&#39;applicazione se ha caricato correttamente la risorsa multimediale.
1. Quando lo stato del lettore multimediale cambia in `INITIALIZED`, potete chiamare `MediaPlayer.prepareToPlay()`.

   Questo stato indica che il supporto è stato caricato correttamente. Il nuovo `MediaPlayerItem` è pronto per la riproduzione. La chiamata `prepareToPlay()` avvia il processo di risoluzione e posizionamento pubblicitario, se presente.

Se si verifica un errore, il lettore multimediale passa allo `ERROR` stato.

Il seguente codice di esempio semplificato illustra il processo di caricamento di una risorsa multimediale:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 
```
