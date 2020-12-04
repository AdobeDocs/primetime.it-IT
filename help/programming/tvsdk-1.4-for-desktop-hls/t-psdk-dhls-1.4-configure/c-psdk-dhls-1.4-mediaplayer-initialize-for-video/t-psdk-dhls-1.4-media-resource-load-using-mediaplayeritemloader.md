---
description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile per ottenere informazioni su un particolare flusso multimediale senza creare un'istanza di MediaPlayer.
seo-description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile per ottenere informazioni su un particolare flusso multimediale senza creare un'istanza di MediaPlayer.
seo-title: Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader
title: Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader
uuid: a7ec8f58-7357-4757-a402-e879dd6caec8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile per ottenere informazioni su un particolare flusso multimediale senza creare un&#39;istanza di MediaPlayer.

Attraverso la classe `MediaPlayerItemLoader`, potete scambiare una risorsa multimediale per la `MediaPlayerItem` corrispondente senza collegare una vista a un&#39;istanza `MediaPlayer`, il che comporterebbe l&#39;allocazione delle risorse hardware di decodifica video. Il processo per ottenere l&#39;istanza `MediaPlayerItem` è asincrono.

1. Implementa i listener di eventi per questi eventi `MediaPlayerItemLoader`:

   * `MediaPlayerItemLoaderEvent.ERROR` event

      TVSDK lo utilizza per informare l’applicazione che si è verificato un errore. TVSDK fornisce una proprietà error contenente informazioni diagnostiche.

1. Registra l&#39;istanza in `MediaPlayerItemLoader`.
1. Chiamare `DefaultMediaPlayerItemLoader.load`, passando un&#39;istanza di un oggetto `MediaResource`.

   L&#39;URL dell&#39;oggetto `MediaResource` deve puntare al flusso per il quale si desidera ottenere informazioni. Ad esempio:

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

