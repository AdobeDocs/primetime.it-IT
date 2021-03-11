---
description: MediaPlayer fornisce i metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.
title: Impostare i tempi di buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Imposta i tempi di buffering{#set-buffering-times}

MediaPlayer fornisce i metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima della riproduzione iniziale, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo di buffer di riproduzione in corso.

1. Impostare l&#39;oggetto `BufferControlParameters`, che incapsula il tempo di buffer iniziale e i parametri di controllo del tempo di buffer di riproduzione:

       Questa classe fornisce i seguenti metodi di fabbrica:
   
   * Per impostare il tempo di buffer iniziale uguale al tempo del buffer di riproduzione:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Per impostare i tempi di buffer iniziali e di riproduzione:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Questi metodi generano un `IllegalArgumentException` se i parametri non sono validi, ad esempio quando:

   * Il tempo di buffer iniziale è inferiore a zero.
   * Il tempo di buffer iniziale è maggiore del tempo di buffer.

1. Per impostare i valori dei parametri del buffer, utilizzare questo metodo `MediaPlayer`:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizza questo metodo `MediaPlayer`:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Ad esempio, per impostare il buffer iniziale a 2 secondi e il tempo del buffer di riproduzione a 30 secondi:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

Questa funzione è illustrata in `psdkdemo` ; utilizzare le impostazioni dell&#39;applicazione per impostare i valori del buffer.
