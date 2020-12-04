---
description: Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.
seo-description: Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.
seo-title: Impostare i tempi di buffering
title: Impostare i tempi di buffering
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Buffering {#buffering}

Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare il modo in cui il lettore bufferizza.

TVSDK definisce un buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale entro il quale, prima dell&#39;avvio della riproduzione del supporto, almeno 2 secondi. Dopo le chiamate dell&#39;applicazione `play` ma prima dell&#39;inizio della riproduzione, TVSDK esegue il buffer dei supporti fino al tempo iniziale per dare un avvio corretto all&#39;avvio effettivo della riproduzione.

È possibile modificare i tempi del buffer definendo nuovi criteri di buffering e modificare il momento in cui si verifica il buffering iniziale utilizzando l&#39;accesso immediato.

## Impostare i tempi di buffering {#set-buffering-times}

`MediaPlayer` fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non impostate i parametri di controllo del buffer prima dell&#39;inizio della riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

1. Impostare l&#39;oggetto `BufferControlParameters`, che racchiude i parametri iniziali di tempo buffer e di controllo del tempo buffer di riproduzione:

       Questa classe fornisce due metodi factory:
   
   * Per impostare la durata iniziale del buffer uguale al tempo del buffer di riproduzione:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Per impostare sia i tempi iniziali che di riproduzione del buffer:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Questi metodi generano un `IllegalArgumentException` se i parametri non sono validi, ad esempio quando:

   * Il tempo iniziale del buffer è inferiore a zero.
   * Il tempo iniziale del buffer è maggiore del tempo del buffer.

1. Per impostare i valori dei parametri del buffer, utilizzare il seguente metodo `MediaPlayer`:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizzate il seguente metodo `MediaPlayer`:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Se AVE non è in grado di impostare i valori specificati, il lettore multimediale immette lo stato `ERROR` con il codice di errore `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Ad esempio, per impostare il buffer iniziale su 2 secondi e il tempo del buffer di riproduzione su 30 secondi:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

L’implementazione di riferimento Primetime dimostra questa funzione; utilizzare le impostazioni dell&#39;applicazione per impostare i valori del buffer.