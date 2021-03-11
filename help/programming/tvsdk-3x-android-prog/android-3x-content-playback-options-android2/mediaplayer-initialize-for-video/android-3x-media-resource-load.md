---
description: Carica una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è un modo per caricare una risorsa multimediale.
title: Caricare una risorsa multimediale nel lettore multimediale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Caricare una risorsa multimediale nel lettore multimediale {#load-a-media-resource-in-the-media-player}

Carica una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è un modo per caricare una risorsa multimediale.

1. Imposta il lettore multimediale per riprodurre la nuova risorsa.

   Sostituisci l&#39;elemento attualmente riproducibile chiamando `MediaPlayer.replaceCurrentResource()` e passando un&#39;istanza `MediaResource` esistente.

   Viene avviato il processo di caricamento delle risorse.

1. Registra l&#39;evento `MediaPlayerEvent.STATUS_CHANGED` con l&#39;istanza `MediaPlayer`. Nel callback, controlla almeno i seguenti valori di stato:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   Attraverso questi eventi, l&#39;oggetto `MediaPlayer` notifica l&#39;applicazione quando la risorsa multimediale è stata caricata correttamente.
1. Quando lo stato del lettore multimediale cambia in `INITIALIZED`, puoi chiamare `MediaPlayer.prepareToPlay()`.

   Questo stato indica che il supporto è stato caricato correttamente. Il nuovo `MediaPlayerItem` è pronto per la riproduzione. Una chiamata a `prepareToPlay()` avvia il processo di risoluzione e posizionamento dei messaggi pubblicitari, se presente.

Se si verifica un errore, il lettore multimediale passa allo stato `ERROR` .

Il seguente codice di esempio semplificato illustra il processo di caricamento di una risorsa multimediale:

```java>
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
