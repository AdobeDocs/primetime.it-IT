---
description: È possibile impostare un solo percorso per gestire gli errori.
title: Configurare la gestione degli errori
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 2%

---


# Imposta la gestione degli errori {#set-up-error-handling}

È possibile impostare un solo percorso per gestire gli errori.

1. Implementa una funzione di callback di un evento per `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull’evento, ad esempio un oggetto `MediaPlayerStatusChangeEvent` .
1. Nel callback, quando lo stato restituito è `MediaPlayerStatus.ERROR`, fornisci logica per gestire tutti gli errori.
1. Dopo aver gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

   Quando l&#39;oggetto `MediaPlayer` si trova nello stato di errore, rimane in tale stato finché non viene reimpostato utilizzando il metodo `MediaPlayer.reset` .

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

