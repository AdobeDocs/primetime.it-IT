---
description: È possibile impostare una posizione per gestire gli errori.
title: Configurare la gestione degli errori
exl-id: 594cd9b8-491f-4972-990a-5657f87c7f89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Configurare la gestione degli errori {#set-up-error-handling}

È possibile impostare una posizione per gestire gli errori.

1. Implementare una funzione di callback dell’evento per `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull’evento, ad esempio `MediaPlayerStatusChangeEvent` oggetto.
1. Nel callback, quando lo stato restituito è `MediaPlayerStatus.ERROR`, forniscono logica per gestire tutti gli errori.
1. Dopo aver gestito l’errore, reimposta il `MediaPlayer` o carica una nuova risorsa multimediale.

   Quando `MediaPlayer` l&#39;oggetto si trova nello stato di errore, ma rimane in tale stato fino a quando non viene reimpostato utilizzando `MediaPlayer.reset` metodo.

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

Ad esempio:

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```
