---
description: MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering della riproduzione.
title: Impostare i tempi di buffering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Impostare i tempi di buffering{#set-buffering-times}

MediaPlayer fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering della riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima di iniziare la riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

1. Configurare `BufferControlParameters` oggetto, che incapsula i parametri di controllo del tempo del buffer iniziale e del tempo del buffer di riproduzione:

       Questa classe fornisce i seguenti metodi di fabbrica:
   
   * Per impostare il tempo del buffer iniziale uguale al tempo del buffer di riproduzione:

     ```
     createSimple(bufferTime:uint):BufferControlParameters
     ```

   * Per impostare i tempi del buffer iniziale e di riproduzione:

     ```
     createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
     ```

     Questi metodi generano un `IllegalArgumentException` se i parametri non sono validi, ad esempio quando:

   * Il tempo del buffer iniziale è inferiore a zero.
   * Il tempo del buffer iniziale è maggiore del tempo del buffer.

1. Per impostare i valori dei parametri del buffer, utilizzare quanto segue `MediaPlayer` metodo:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizzare quanto segue `MediaPlayer` metodo:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Ad esempio, per impostare il buffer iniziale su 2 secondi e il tempo del buffer di riproduzione su 30 secondi:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

Il `psdkdemo` viene illustrata questa funzione; utilizzare le impostazioni dell&#39;applicazione per impostare i valori del buffer.
