---
description: Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa opzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un'istanza di MediaPlayer.
title: Caricare una risorsa multimediale tramite MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Caricare una risorsa multimediale tramite MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Un altro modo per risolvere una risorsa multimediale è con MediaPlayerItemLoader. Questa opzione è utile quando si desidera ottenere informazioni su un particolare flusso multimediale senza creare un&#39;istanza di MediaPlayer.

Attraverso il `MediaPlayerItemLoader` , è possibile scambiare una risorsa multimediale con la corrispondente `MediaPlayerItem` senza associare una visualizzazione a un `MediaPlayer` che porterebbe all&#39;allocazione delle risorse hardware di decodifica video. Il processo di ottenimento `MediaPlayerItem` l&#39;istanza è asincrona.

1. Implementare `MediaPlayerItemLoader.LoaderListener` interfaccia di callback.

       Questa interfaccia definisce due metodi:
   
   * `LoaderListener.onError` funzione di callback

     TVSDK utilizza questa funzione per informare l’applicazione che si è verificato un errore. TVSDK fornisce un codice di errore come parametri e una stringa di descrizione che contiene informazioni di diagnostica.

   * `LoaderListener.onError` funzione di callback

     TVSDK utilizza questo per informare l’applicazione che le informazioni richieste sono disponibili sotto forma di `MediaPlayerItem` istanza passata come parametro al callback.

1. Registra questa istanza in TVSDK trasmettendola come parametro al costruttore del `MediaPlayerItemLoader`.
1. Chiamata `MediaPlayerItemLoader.load`, passaggio di un&#39;istanza di un `MediaResource` oggetto.

   L’URL del `MediaResource` L&#39;oggetto deve puntare al flusso per il quale si desidera ottenere informazioni. Ad esempio:

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
