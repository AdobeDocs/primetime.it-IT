---
description: Carica una risorsa creando direttamente un'istanza di MediaResource e caricando il contenuto video da riprodurre.
title: Caricare una risorsa multimediale in MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Caricare una risorsa multimediale in MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carica una risorsa creando direttamente un&#39;istanza di MediaResource e caricando il contenuto video da riprodurre.

1. Imposta l&#39;elemento riproducibile dell&#39;oggetto `MediaPlayer` con la nuova risorsa da riprodurre.

   Sostituisci l&#39;elemento attualmente riproducibile dell&#39;oggetto `MediaPlayer` esistente chiamando `replaceCurrentResource` e passando un&#39;istanza `MediaResource` esistente.

1. Attendi che il browser TVSDK invii `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status` che è uguale a uno dei seguenti:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Attraverso questi eventi, l&#39;oggetto MediaPlayer notifica all&#39;applicazione se la risorsa multimediale è stata caricata correttamente.

1. Quando lo stato del lettore multimediale cambia in `MediaPlayerStatus.INITIALIZED`, puoi chiamare `MediaPlayer.prepareToPlay`.

   Lo stato INITIALIZED indica che il supporto è stato caricato correttamente. Una chiamata a `prepareToPlay` avvia il processo di risoluzione e posizionamento dei messaggi pubblicitari, se presente.
1. Quando il browser TVSDK invia l&#39;evento `MediaPlayerStatus.PREPARED` il flusso multimediale è stato caricato correttamente (viene creato un MediaPlayerItem) ed è pronto per la riproduzione.

Se si verifica un errore, il `MediaPlayer` passa al `MediaPlayerStatus.ERROR`.

Invia inoltre una notifica all&#39;applicazione inviando l&#39;evento `MediaPlayerStatus.ERROR` .

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
