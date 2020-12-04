---
description: Configurate un'unica posizione per gestire gli errori.
seo-description: Configurate un'unica posizione per gestire gli errori.
seo-title: Impostazione della gestione degli errori
title: Impostazione della gestione degli errori
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# Impostazione della gestione degli errori{#set-up-error-handling}

Configurate un&#39;unica posizione per gestire gli errori.

1. Implementare una funzione di callback dell&#39;evento per `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull&#39;evento, ad esempio un oggetto `MediaPlayerStatusChangeEvent`.
1. Nel callback, quando lo stato restituito è `MediaPlayerState.ERROR`, fornire logica per gestire tutti gli errori.
1. Una volta gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

   Quando l&#39;oggetto `MediaPlayer` è in stato di errore, rimane in tale stato finché non viene reimpostato utilizzando il metodo `MediaPlayer.reset`.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Ad esempio:

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```

