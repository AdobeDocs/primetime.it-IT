---
description: Configurate un'unica posizione per gestire gli errori.
seo-description: Configurate un'unica posizione per gestire gli errori.
seo-title: Impostazione della gestione degli errori
title: Impostazione della gestione degli errori
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 1%

---


# Impostazione della gestione degli errori{#set-up-error-handling}

Configurate un&#39;unica posizione per gestire gli errori.

1. Implementare una funzione di callback dell&#39;evento per `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull&#39;evento, ad esempio un oggetto `MediaPlayerStatusChangeEvent`.
1. Nel callback, quando lo stato dal parametro event è `MediaPlayerStatus.ERROR`, fornire logica per gestire tutti gli errori.
1. Una volta gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

   Se l&#39;oggetto `MediaPlayer` è in stato di errore, non può uscire da questo stato finché non si reimposta l&#39;oggetto `MediaPlayer` (tramite il metodo `MediaPlayer.reset`) o si carica una nuova risorsa multimediale ( `MediaPlayer.replaceCurrentItem`).

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

