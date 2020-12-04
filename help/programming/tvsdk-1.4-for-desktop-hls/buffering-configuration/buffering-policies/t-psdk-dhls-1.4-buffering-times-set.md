---
description: MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.
seo-description: MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.
seo-title: Impostare i tempi di buffering
title: Impostare i tempi di buffering
uuid: 25142b01-5381-49c9-b89a-24c858faaf13
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Impostare i tempi di buffering{#set-buffering-times}

MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non impostate i parametri di controllo del buffer prima dell&#39;inizio della riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

1. Impostare l&#39;oggetto `BufferControlParameters`, che racchiude i parametri iniziali di tempo buffer e di controllo del tempo buffer di riproduzione:

       Questa classe fornisce i seguenti metodi factory:
   
   * Per impostare la durata iniziale del buffer uguale al tempo del buffer di riproduzione:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Per impostare sia i tempi iniziali che di riproduzione del buffer:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Questi metodi generano un `IllegalArgumentException` se i parametri non sono validi, ad esempio quando:

   * Il tempo iniziale del buffer è inferiore a zero.
   * Il tempo iniziale del buffer è maggiore del tempo del buffer.

1. Per impostare i valori dei parametri del buffer, utilizzare il seguente metodo `MediaPlayer`:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizzate il seguente metodo `MediaPlayer`:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Ad esempio, per impostare il buffer iniziale su 2 secondi e il tempo del buffer di riproduzione su 30 secondi:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

La `psdkdemo` illustra questa funzione; utilizzare le impostazioni dell&#39;applicazione per impostare i valori del buffer.
