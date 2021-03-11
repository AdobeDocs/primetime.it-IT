---
description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un'istanza MediaPlayer.
title: Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa funzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un&#39;istanza MediaPlayer.

Attraverso la classe `MediaPlayerItemLoader` è possibile scambiare una risorsa multimediale per la corrispondente `MediaPlayerItem` senza allegare una visualizzazione a un&#39;istanza `MediaPlayer`, il che porterebbe all&#39;allocazione delle risorse hardware di decodifica video. Il processo di ottenimento dell&#39;istanza `MediaPlayerItem` è asincrono.

1. Implementa l’interfaccia di callback `MediaPlayerItemLoader.LoaderListener` .

       Questa interfaccia definisce due metodi:
   
   * `LoaderListener.onError` funzione di callback

      TVSDK lo utilizza per informare l&#39;applicazione che si è verificato un errore. TVSDK fornisce un codice di errore come parametri e una stringa di descrizione contenente informazioni di diagnostica.

   * `LoaderListener.onError` funzione di callback

      TVSDK lo utilizza per informare l&#39;applicazione che le informazioni richieste sono disponibili sotto forma di un&#39;istanza `MediaPlayerItem` che viene passata come parametro al callback.

1. Registra questa istanza in TVSDK trasmettendola come parametro al costruttore del `MediaPlayerItemLoader`.
1. Chiama `MediaPlayerItemLoader.load`, passando un&#39;istanza di un oggetto `MediaResource`.

   L&#39;URL dell&#39;oggetto `MediaResource` deve puntare al flusso di cui si desidera ottenere le informazioni. Ad esempio:

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

