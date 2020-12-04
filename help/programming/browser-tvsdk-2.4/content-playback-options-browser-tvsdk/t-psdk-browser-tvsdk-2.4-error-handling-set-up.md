---
description: È possibile impostare una posizione nell'applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.
seo-description: È possibile impostare una posizione nell'applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.
seo-title: Impostazione della gestione degli errori
title: Impostazione della gestione degli errori
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 2%

---


# Impostazione della gestione degli errori{#set-up-error-handling}

È possibile impostare una posizione nell&#39;applicazione per eseguire la gestione degli errori in risposta allo stato ERROR.

1. Aggiungete un listener di eventi per `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Ad esempio:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. Nel listener di eventi, quando `event.status` è `AdobePSDK.MediaPlayerStatus.ERROR`, fornire la logica necessaria per gestire tutti gli errori.
1. Una volta gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

       Quando l&#39;oggetto MediaPlayer è in stato di errore, non può uscire da tale stato finché non si completa una delle seguenti attività:
   
   * Reimpostare l&#39;oggetto MediaPlayer utilizzando il metodo `MediaPlayer.reset`.
   * Caricate una nuova risorsa multimediale utilizzando il metodo `MediaPlayer.replaceCurrentResource`.

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

