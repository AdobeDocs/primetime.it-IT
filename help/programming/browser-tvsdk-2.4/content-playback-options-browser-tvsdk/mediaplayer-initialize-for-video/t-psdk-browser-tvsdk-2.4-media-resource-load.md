---
description: Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre.
title: Caricare una risorsa multimediale in MediaPlayer
exl-id: b775c33e-399c-4a03-a132-407944f07706
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Caricare una risorsa multimediale in MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carica una risorsa creando direttamente un’istanza di MediaResource e caricando il contenuto video da riprodurre.

1. Imposta il `MediaPlayer` elemento riproducibile dell’oggetto con la nuova risorsa da riprodurre.

   Sostituisci il tuo esistente `MediaPlayer` elemento attualmente riproducibile dell’oggetto chiamando `replaceCurrentResource` e il passaggio di un `MediaResource` dell&#39;istanza.

1. Attesa dell&#39;invio di TVSDK per il browser `AdobePSDK.MediaPlayerStatusChangeEvent` con `event.status` uguale a uno dei seguenti:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Attraverso questi eventi, l&#39;oggetto MediaPlayer notifica all&#39;applicazione se la risorsa multimediale è stata caricata correttamente.

1. Quando lo stato del lettore multimediale cambia in `MediaPlayerStatus.INITIALIZED`, è possibile chiamare `MediaPlayer.prepareToPlay`.

   Lo stato INIZIALIZZATO indica che il supporto è stato caricato correttamente. Chiamata `prepareToPlay` avvia il processo di risoluzione e posizionamento pubblicitario, se presente.
1. Quando il TVSDK del browser invia `MediaPlayerStatus.PREPARED` evento caricato correttamente dal flusso multimediale (viene creato MediaPlayerItem) e preparato per la riproduzione.

Se si verifica un errore, il `MediaPlayer` passa a `MediaPlayerStatus.ERROR`.

Notifica inoltre l’applicazione inviando `MediaPlayerStatus.ERROR` evento.

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
