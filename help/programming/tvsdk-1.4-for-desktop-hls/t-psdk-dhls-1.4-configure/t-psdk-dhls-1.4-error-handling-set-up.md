---
description: Imposta un'unica posizione per gestire gli errori.
title: Configurare la gestione degli errori
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 2%

---


# Imposta la gestione degli errori{#set-up-error-handling}

Imposta un&#39;unica posizione per gestire gli errori.

1. Implementa una funzione di callback di un evento per `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull’evento, ad esempio un oggetto `MediaPlayerStatusChangeEvent` .
1. Nel callback, quando lo stato del parametro dell&#39;evento è `MediaPlayerStatus.ERROR`, fornisci logica per gestire tutti gli errori.
1. Dopo aver gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

   Quando l&#39;oggetto `MediaPlayer` si trova nello stato ERROR, non può uscire da questo stato finché non si reimposta l&#39;oggetto `MediaPlayer` (tramite il metodo `MediaPlayer.reset`) o si carica una nuova risorsa multimediale ( `MediaPlayer.replaceCurrentItem`).

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Ad esempio:

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```

