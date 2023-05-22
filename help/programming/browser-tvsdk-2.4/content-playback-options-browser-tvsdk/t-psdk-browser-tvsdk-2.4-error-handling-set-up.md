---
description: È possibile impostare una posizione nell'applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.
title: Configurare la gestione degli errori
exl-id: c0ce1d80-85d5-4344-9ab0-bd56906421cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
