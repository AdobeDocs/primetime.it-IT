---
description: L'utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un'istanza di MediaPlayer. Questa funzione è particolarmente utile nei flussi di pre-buffering, in modo che la riproduzione possa iniziare senza ritardi.
title: Caricare una risorsa multimediale tramite MediaPlayerItemLoader
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Caricare una risorsa multimediale tramite MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

L&#39;utilizzo di MediaPlayerItemLoader consente di ottenere informazioni su un flusso multimediale senza creare un&#39;istanza di MediaPlayer. Questa funzione è particolarmente utile nei flussi di pre-buffering, in modo che la riproduzione possa iniziare senza ritardi.

Il `MediaPlayerItemLoader` questa classe consente di scambiare una risorsa multimediale con la `MediaPlayerItem` senza associare una visualizzazione a un `MediaPlayer` che alloca risorse hardware di decodifica video. Sono necessari ulteriori passaggi per i contenuti protetti da DRM, ma il presente manuale non li descrive.

>[!IMPORTANT]
>
>TVSDK non supporta un `QoSProvider` per lavorare con entrambi `itemLoader` e `MediaPlayer`. Se l&#39;applicazione utilizza Instant On, l&#39;applicazione deve mantenere due `QoS` e gestiscono entrambe le istanze per le informazioni. Consulta [Istantanea attiva](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) per ulteriori informazioni.

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
   >Crea un&#39;istanza separata di `MediaPlayerItemLoader` per ogni risorsa. Non utilizzarne uno `MediaPlayerItemLoader` per caricare più risorse.

1. Implementare `ItemLoaderListener` classe per ricevere notifiche da `MediaPlayerItemLoader` dell&#39;istanza.

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

   In `onLoadComplete()` callback, eseguire una delle operazioni seguenti:

   * Assicurati che tutto ciò che potrebbe influenzare il buffering, ad esempio la selezione di tracce WebVTT o audio, sia completo e chiama `prepareBuffer()` per usufruire di instant on.
   * Allega l&#39;elemento al `MediaPlayer` istanza tramite `replaceCurrentItem()`.

   Se chiami `prepareBuffer()`, si riceve l&#39;evento BUFFER_READY nel `onBufferPrepared` al termine della preparazione.
1. Chiamata `load` il `MediaPlayerItemLoader` e passare la risorsa da caricare, e facoltativamente l’ID contenuto e un `MediaPlayerItemConfig` dell&#39;istanza.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Per memorizzare il buffer da un punto diverso dall’inizio del flusso, chiama `prepareBuffer()` con la posizione (in millisecondi) in cui avviare il buffering.
1. Utilizza il `replaceCurrentItem()` e `play()` metodi di `MediaPlayer` per iniziare la riproduzione da quel punto.
1. Attendi stato di inattività e chiama `replaceCurrentItem`.
1. Riproduci l&#39;elemento.

   * Se l’elemento viene caricato ma non inserito nel buffer:

      1. Attendere lo stato inizializzato.
      1. Chiamata `prepareToPlay()`.
      1. Attendere lo stato READY.
      1. Chiamata `play()`.

   * Se l’elemento è inserito nel buffer:

      1. Attendere l&#39;evento di preparazione del buffer.
      1. Chiamata `play()`.
