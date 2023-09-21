---
description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa opzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un'istanza di MediaPlayer.
title: Caricare una risorsa multimediale tramite MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Caricare una risorsa multimediale tramite MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa opzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un&#39;istanza di MediaPlayer.

Attraverso il `MediaPlayerItemLoader` , è possibile scambiare una risorsa multimediale con la corrispondente `MediaPlayerItem` senza associare una visualizzazione a un `MediaPlayer` che porterebbe all&#39;allocazione delle risorse hardware di decodifica video. Il processo di ottenimento `MediaPlayerItem` l&#39;istanza è asincrona.

1. Implementa listener di eventi per questi `MediaPlayerItemLoader` Eventi:

   * `MediaPlayerItemLoaderEvent.ERROR` evento

     TVSDK utilizza questa funzione per informare l’applicazione che si è verificato un errore. TVSDK fornisce una proprietà di errore che contiene informazioni di diagnostica.

1. Registra questa istanza in `MediaPlayerItemLoader`.
1. Chiamata `DefaultMediaPlayerItemLoader.load`, passaggio di un&#39;istanza di un `MediaResource` oggetto.

   L’URL del `MediaResource` L&#39;oggetto deve puntare al flusso per il quale si desidera ottenere informazioni. Ad esempio:

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
