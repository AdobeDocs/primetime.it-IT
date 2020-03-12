---
description: È possibile impostare un percorso per gestire gli errori.
seo-description: È possibile impostare un percorso per gestire gli errori.
seo-title: Impostazione della gestione degli errori
title: Impostazione della gestione degli errori
uuid: 7c122830-6259-4e95-882e-fb1700454e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Impostazione della gestione degli errori {#set-up-error-handling}

È possibile impostare un percorso per gestire gli errori.

1. Implementare una funzione di callback dell&#39;evento per `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull&#39;evento, ad esempio un `MediaPlayerStatusChangeEvent` oggetto.
1. Nel callback, quando lo stato restituito è `MediaPlayerStatus.ERROR`, fornire logica per gestire tutti gli errori.
1. Una volta gestito l&#39;errore, reimpostare l&#39; `MediaPlayer` oggetto o caricare una nuova risorsa multimediale.

   Quando l&#39; `MediaPlayer` oggetto si trova nello stato di errore, rimane nello stato finché non viene reimpostato utilizzando il `MediaPlayer.reset` metodo.

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
