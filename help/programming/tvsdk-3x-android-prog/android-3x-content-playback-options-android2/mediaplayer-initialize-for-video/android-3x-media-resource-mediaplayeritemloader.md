---
description: L'utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un'istanza MediaPlayer. Questa funzione è particolarmente utile nei flussi di pre-buffering, in modo che la riproduzione possa iniziare immediatamente.
title: Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

L&#39;utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un&#39;istanza MediaPlayer. Questa funzione è particolarmente utile nei flussi di pre-buffering, in modo che la riproduzione possa iniziare immediatamente.

La classe `MediaPlayerItemLoader` consente di scambiare una risorsa multimediale per la `MediaPlayerItem` corrente senza allegare una visualizzazione a un&#39;istanza `MediaPlayer`, che allocerebbe le risorse hardware di decodifica video. Sono necessari ulteriori passaggi per i contenuti protetti da DRM, ma questo manuale non li descrive.

>[!IMPORTANT]
>
>TVSDK non supporta un singolo `QoSProvider` per funzionare sia con `itemLoader` che con `MediaPlayer`. Se l&#39;applicazione utilizza Instant On, l&#39;applicazione deve mantenere due istanze `QoS` e gestire entrambe le istanze per le informazioni. Per ulteriori informazioni, consulta [Instant-on](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) .

1. Crea un&#39;istanza di `MediaPlayerItemLoader`.

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
   >Crea un&#39;istanza separata di `MediaPlayerItemLoader` per ogni risorsa. Non utilizzare un&#39;istanza `MediaPlayerItemLoader` per caricare più risorse.

1. Implementa la classe `ItemLoaderListener` per ricevere notifiche dall&#39;istanza `MediaPlayerItemLoader`.

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

   Nel callback `onLoadComplete()` , effettua una delle seguenti operazioni:

   * Assicurati che tutto ciò che potrebbe influenzare il buffering, ad esempio la selezione di tracce WebVTT o audio, sia completo e chiama `prepareBuffer()` per sfruttare l&#39;accesso immediato.
   * Allega l’elemento all’istanza `MediaPlayer` utilizzando `replaceCurrentItem()`.

   Se si chiama `prepareBuffer()`, al termine della preparazione si riceve l&#39;evento BUFFER_PREPARED nel gestore `onBufferPrepared`.
1. Chiama `load` sull&#39;istanza `MediaPlayerItemLoader` e passa la risorsa da caricare, ed eventualmente l&#39;ID del contenuto e un&#39;istanza `MediaPlayerItemConfig`.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Per eseguire il buffer da un punto diverso dall&#39;inizio del flusso, chiamare `prepareBuffer()` con la posizione (in millisecondi) in cui avviare il buffering.
1. Utilizza i metodi `replaceCurrentItem()` e `play()` di `MediaPlayer` per iniziare a riprodurre da quel momento.
1. Attendi lo stato di inattività e chiama `replaceCurrentItem`.
1. Riproduci l&#39;elemento.

   * Se l’elemento viene caricato ma non inserito nel buffer:

      1. Attendi lo stato inizializzato.
      1. Chiama `prepareToPlay()`.
      1. Attendere lo stato PREPARATO.
      1. Chiama `play()`.
   * Se l’elemento è bufferizzato:

      1. Attendi l&#39;evento preparato del buffer.
      1. Chiama `play()`.