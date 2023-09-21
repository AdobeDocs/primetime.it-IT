---
description: È possibile impostare una posizione nell'applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.
title: Configurare la gestione degli errori
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Configurare la gestione degli errori{#set-up-error-handling}

È possibile impostare una posizione nell&#39;applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.

1. Aggiungere un listener di eventi per `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Ad esempio:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. Nel listener di eventi, quando `event.status` è `AdobePSDK.MediaPlayerStatus.ERROR`, specifica la logica per gestire tutti gli errori.
1. Dopo aver gestito l’errore, reimposta il `MediaPlayer` o carica una nuova risorsa multimediale.

       Quando l&#39;oggetto MediaPlayer è nello stato ERROR, non può uscire da questo stato finché non viene completata una delle seguenti attività:
   
   * Reimpostare l&#39;oggetto MediaPlayer utilizzando `MediaPlayer.reset` metodo.
   * Caricare una nuova risorsa multimediale utilizzando `MediaPlayer.replaceCurrentResource` metodo.

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

Ad esempio:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```
