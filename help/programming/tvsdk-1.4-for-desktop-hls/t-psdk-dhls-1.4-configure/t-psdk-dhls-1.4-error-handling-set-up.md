---
description: Imposta un'unica posizione per gestire gli errori.
title: Configurare la gestione degli errori
exl-id: ce4a2954-0166-43af-afdf-0aa24659f1ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Configurare la gestione degli errori{#set-up-error-handling}

Imposta un&#39;unica posizione per gestire gli errori.

1. Implementare una funzione di callback dell’evento per `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull’evento, ad esempio `MediaPlayerStatusChangeEvent` oggetto.
1. Nel callback, quando lo stato dal parametro evento è `MediaPlayerStatus.ERROR`, forniscono logica per gestire tutti gli errori.
1. Dopo aver gestito l’errore, reimposta il `MediaPlayer` o carica una nuova risorsa multimediale.

   Quando `MediaPlayer` l&#39;oggetto è nello stato ERROR, non può uscire da questo stato finché non viene reimpostato `MediaPlayer` oggetto (tramite `MediaPlayer.reset` o carica una nuova risorsa multimediale ( `MediaPlayer.replaceCurrentItem`).

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
