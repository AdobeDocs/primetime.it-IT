---
description: Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.
title: Caricare una risorsa multimediale nel lettore multimediale
exl-id: f39d3aa2-8912-4dac-9f10-91b6d20395ea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Caricare una risorsa multimediale nel lettore multimediale {#load-a-media-resource-in-the-media-player}

Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre. Questo è uno dei modi per caricare una risorsa multimediale.

1. Imposta il lettore multimediale per riprodurre la nuova risorsa.

   Sostituisci l’elemento attualmente riproducibile chiamando `MediaPlayer.replaceCurrentResource()` e il passaggio di un `MediaResource` dell&#39;istanza.

   Verrà avviato il processo di caricamento delle risorse.

1. Registra il `MediaPlayerEvent.STATUS_CHANGED` evento con `MediaPlayer` dell&#39;istanza. Nel callback, verifica la presenza almeno dei seguenti valori di stato:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   Attraverso questi eventi, il `MediaPlayer` L&#39;oggetto avvisa l&#39;applicazione quando la risorsa multimediale è stata caricata correttamente.
1. Quando lo stato del lettore multimediale cambia in `INITIALIZED`, è possibile chiamare `MediaPlayer.prepareToPlay()`.

   Questo stato indica che il supporto è stato caricato correttamente. Il nuovo `MediaPlayerItem` è pronto per la riproduzione. Chiamata `prepareToPlay()` avvia il processo di risoluzione e posizionamento pubblicitario, se presente.

Se si verifica un errore, il lettore multimediale passa alla `ERROR` stato.

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
