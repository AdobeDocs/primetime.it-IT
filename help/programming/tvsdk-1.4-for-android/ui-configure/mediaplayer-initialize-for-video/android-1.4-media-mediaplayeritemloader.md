---
description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile per ottenere informazioni su un particolare flusso multimediale senza creare un'istanza di MediaPlayer.
seo-description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile per ottenere informazioni su un particolare flusso multimediale senza creare un'istanza di MediaPlayer.
seo-title: Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader
title: Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile per ottenere informazioni su un particolare flusso multimediale senza creare un&#39;istanza di MediaPlayer.

Attraverso la `MediaPlayerItemLoader` classe, potete scambiare una risorsa multimediale per la risorsa corrispondente `MediaPlayerItem` senza allegare una vista a un&#39; `MediaPlayer` istanza, il che comporterebbe l&#39;allocazione delle risorse hardware di decodifica video. Il processo di ottenimento dell&#39; `MediaPlayerItem` istanza è asincrono.

1. Implementa l’interfaccia di `MediaPlayerItemLoader.LoaderListener` callback.

       Questa interfaccia definisce due metodi:
   
   * `LoaderListener.onError` funzione di callback

      TVSDK lo utilizza per informare l’applicazione che si è verificato un errore. TVSDK fornisce un codice di errore come parametri e una stringa di descrizione che contiene informazioni diagnostiche.

   * `LoaderListener.onError` funzione di callback

      TVSDK utilizza questo metodo per informare l’applicazione che le informazioni richieste sono disponibili sotto forma di `MediaPlayerItem` istanza che viene passata come parametro al callback.

1. Registra questa istanza in TVSDK trasmettendola come parametro al costruttore del `MediaPlayerItemLoader`.
1. Chiamata `MediaPlayerItemLoader.load`, passaggio di un&#39;istanza di un `MediaResource` oggetto.

   L&#39;URL dell&#39; `MediaResource` oggetto deve puntare al flusso per il quale si desidera ottenere informazioni. Ad esempio:

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

