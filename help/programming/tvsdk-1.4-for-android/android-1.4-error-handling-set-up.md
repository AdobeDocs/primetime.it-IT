---
description: Imposta un'unica posizione per gestire gli errori.
title: Configurare la gestione degli errori
exl-id: 2d0e0d08-d932-4b6e-8f95-494a2e666827
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Configurare la gestione degli errori{#set-up-error-handling}

Imposta un&#39;unica posizione per gestire gli errori.

1. Implementare una funzione di callback dell’evento per `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull’evento, ad esempio `MediaPlayerStatusChangeEvent` oggetto.
1. Nel callback, quando lo stato restituito è `MediaPlayerState.ERROR`, forniscono logica per gestire tutti gli errori.
1. Dopo aver gestito l’errore, reimposta il `MediaPlayer` o carica una nuova risorsa multimediale.

   Quando `MediaPlayer` l&#39;oggetto è nello stato di errore, rimane in tale stato fino a quando non viene reimpostato utilizzando `MediaPlayer.reset` metodo.

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
