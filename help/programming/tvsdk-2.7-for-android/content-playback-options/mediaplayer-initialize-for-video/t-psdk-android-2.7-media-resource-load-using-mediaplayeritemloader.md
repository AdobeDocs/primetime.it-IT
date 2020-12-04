---
description: L’utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un’istanza di MediaPlayer. Questa funzione è particolarmente utile nei flussi pre-buffering, in modo che la riproduzione possa iniziare senza ritardi.
seo-description: L’utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un’istanza di MediaPlayer. Questa funzione è particolarmente utile nei flussi pre-buffering, in modo che la riproduzione possa iniziare senza ritardi.
seo-title: Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader
title: Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader
uuid: 43ca2470-1fd2-4f66-94fe-a12ed17b52d7
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Caricamento di una risorsa multimediale tramite MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

L’utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un’istanza di MediaPlayer. Questa funzione è particolarmente utile nei flussi pre-buffering, in modo che la riproduzione possa iniziare senza ritardi.

La classe `MediaPlayerItemLoader` consente di scambiare una risorsa multimediale per la `MediaPlayerItem` corrente senza associare una vista a un&#39;istanza `MediaPlayer`, che alloca risorse hardware per la decodifica video. Per i contenuti protetti da DRM sono necessari ulteriori passaggi, che tuttavia non vengono descritti in questo manuale.

>[!IMPORTANT]
>
>TVSDK non supporta un singolo `QoSProvider` per lavorare con `itemLoader` e `MediaPlayer`. Se l&#39;applicazione utilizza Instant On, l&#39;applicazione deve mantenere due istanze `QoS` e gestire entrambe le istanze per le informazioni. Per ulteriori informazioni, vedere [instant-on](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md).

1. Create un&#39;istanza di `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >Create un&#39;istanza separata di `MediaPlayerItemLoader` per ciascuna risorsa. Non utilizzate un&#39;istanza `MediaPlayerItemLoader` per caricare più risorse.

1. Implementate la classe `ItemLoaderListener` per ricevere le notifiche dall&#39;istanza `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   Nel callback `onLoadComplete()`, effettuate una delle seguenti operazioni:

   * Assicurati che tutto ciò che potrebbe influenzare il buffering, ad esempio la selezione di tracce WebVTT o audio, sia completo e chiama `prepareBuffer()` per sfruttare immediatamente.
   * Collegare l&#39;elemento all&#39;istanza `MediaPlayer` utilizzando `replaceCurrentItem()`.

   Se si chiama `prepareBuffer()`, al termine della preparazione viene visualizzato l&#39;evento BUFFER_PREPARED nel gestore `onBufferPrepared`.

1. Chiamare `load` sull&#39;istanza `MediaPlayerItemLoader` e passare la risorsa da caricare, e facoltativamente l&#39;ID contenuto e un&#39;istanza `MediaPlayerItemConfig`.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Per eseguire il buffer da un punto diverso dall&#39;inizio del flusso, chiamare `prepareBuffer()` con la posizione (in millisecondi) in cui avviare il buffering.
1. Utilizzare i metodi `replaceCurrentItem()` e `play()` di `MediaPlayer` per avviare la riproduzione da tale punto.
1. Attendere lo stato di inattività e chiamare `replaceCurrentItem`.
1. Riproduci l’elemento.

   * Se l’elemento viene caricato ma non inserito nel buffer:

      1. Attendere lo stato inizializzato.
      1. Chiama `prepareToPlay()`.
      1. Attendere lo stato PREPARATO.
      1. Chiama `play()`.
   * Se l’elemento è incluso nel buffer:

      1. Attendere l&#39;evento di preparazione del buffer.
      1. Chiama `play()`.