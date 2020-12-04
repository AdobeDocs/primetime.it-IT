---
description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre.
seo-description: Caricate una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre.
seo-title: Caricamento di una risorsa multimediale in MediaPlayer
title: Caricamento di una risorsa multimediale in MediaPlayer
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 7d61a6cd8cb2c381f85a19d9ccac3d235ffceaf1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Caricare una risorsa multimediale in MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Caricate una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre.

1. Impostate l&#39;elemento riproducibile dell&#39;oggetto `MediaPlayer` con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento `MediaPlayer` attualmente riproducibile dell&#39;oggetto esistente chiamando `replaceCurrentResource` e passando un&#39;istanza `MediaResource` esistente.

1. Attendete che l&#39;SDK per browser TVSDK invii `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status` uguale a uno dei seguenti elementi:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Attraverso questi eventi, l&#39;oggetto MediaPlayer comunica all&#39;applicazione se la risorsa multimediale è stata caricata correttamente.

1. Quando lo stato del lettore multimediale diventa `MediaPlayerStatus.INITIALIZED`, è possibile chiamare `MediaPlayer.prepareToPlay`.

   Lo stato INITIALIZED indica che il supporto è stato caricato correttamente. La chiamata di `prepareToPlay` avvia la risoluzione e il processo di posizionamento della pubblicità, se presente.
1. Quando Browser TVSDK invia l&#39;evento `MediaPlayerStatus.PREPARED` il flusso multimediale è stato caricato correttamente (viene creato un oggetto MediaPlayerItem) ed è pronto per la riproduzione.

Se si verifica un errore, `MediaPlayer` passa alla `MediaPlayerStatus.ERROR`.

Inoltre, invia una notifica all&#39;applicazione inviando l&#39;evento `MediaPlayerStatus.ERROR`.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->


Il seguente codice di esempio semplificato illustra il processo di caricamento di una risorsa multimediale:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
