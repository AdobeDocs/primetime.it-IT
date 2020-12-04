---
description: È possibile impostare un percorso per gestire gli errori.
seo-description: È possibile impostare un percorso per gestire gli errori.
seo-title: Impostazione della gestione degli errori
title: Impostazione della gestione degli errori
uuid: fde47fa5-5ca5-4be5-a7e7-3227c5e4c670
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# Impostazione della gestione degli errori {#set-up-error-handling}

È possibile impostare un percorso per gestire gli errori.

1. Implementare una funzione di callback dell&#39;evento per `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK trasmette le informazioni sull&#39;evento, ad esempio un oggetto `MediaPlayerStatusChangeEvent`.
1. Nel callback, quando lo stato restituito è `MediaPlayerStatus.ERROR`, fornire logica per gestire tutti gli errori.
1. Una volta gestito l&#39;errore, reimpostare l&#39;oggetto `MediaPlayer` o caricare una nuova risorsa multimediale.

   Quando l&#39;oggetto `MediaPlayer` è nello stato di errore, rimane nello stato finché non viene reimpostato utilizzando il metodo `MediaPlayer.reset`.

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

