---
description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un'istanza MediaPlayer.
title: Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un&#39;istanza MediaPlayer.

Attraverso la classe `MediaPlayerItemLoader` è possibile scambiare una risorsa multimediale per la corrispondente `MediaPlayerItem` senza allegare una visualizzazione a un&#39;istanza `MediaPlayer`, il che porterebbe all&#39;allocazione delle risorse hardware di decodifica video. Il processo di ottenimento dell&#39;istanza `MediaPlayerItem` è asincrono.

1. Implementa i listener di eventi per questi eventi `MediaPlayerItemLoader`:

   * `MediaPlayerItemLoaderEvent.ERROR` event

      TVSDK lo utilizza per informare l&#39;applicazione che si è verificato un errore. TVSDK fornisce una proprietà di errore contenente informazioni di diagnostica.

1. Registra l&#39;istanza in `MediaPlayerItemLoader`.
1. Chiama `DefaultMediaPlayerItemLoader.load`, passando un&#39;istanza di un oggetto `MediaResource`.

   L&#39;URL dell&#39;oggetto `MediaResource` deve puntare al flusso di cui si desidera ottenere le informazioni. Ad esempio:

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

