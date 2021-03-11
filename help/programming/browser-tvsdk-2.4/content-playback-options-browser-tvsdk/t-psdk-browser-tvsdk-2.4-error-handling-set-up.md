---
description: È possibile impostare una posizione nell'applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.
title: Configurare la gestione degli errori
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 3%

---


# Imposta la gestione degli errori{#set-up-error-handling}

È possibile impostare una posizione nell&#39;applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.

1. Aggiungi un listener di eventi per `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Ad esempio:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. Nel listener di eventi, quando `event.status` è `AdobePSDK.MediaPlayerStatus.ERROR`, fornisci la logica necessaria per gestire tutti gli errori.
1. Dopo aver gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

       Quando l&#39;oggetto MediaPlayer è in stato ERROR, non può uscire da questo stato finché non si completa una delle seguenti attività:
   
   * Reimpostare l&#39;oggetto MediaPlayer utilizzando il metodo `MediaPlayer.reset` .
   * Carica una nuova risorsa multimediale utilizzando il metodo `MediaPlayer.replaceCurrentResource` .

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

