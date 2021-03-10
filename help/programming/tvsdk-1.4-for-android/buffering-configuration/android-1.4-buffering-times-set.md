---
description: Per fornire un’esperienza di visualizzazione più fluida, a volte TVSDK carica il flusso video. Puoi configurare il modo in cui il lettore buffer.
title: Impostare i tempi di buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Buffering {#buffering}

Per fornire un’esperienza di visualizzazione più fluida, a volte TVSDK carica il flusso video. Puoi configurare il modo in cui il lettore buffer.

TVSDK definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale entro tale periodo, prima che il supporto inizi la riproduzione, di almeno 2 secondi. Dopo che l&#39;applicazione chiama `play` ma prima dell&#39;inizio della riproduzione, TVSDK carica il contenuto multimediale fino al tempo iniziale per dare un avvio fluido quando inizia effettivamente la riproduzione.

È possibile modificare i tempi di buffer definendo nuovi criteri di buffering e modificare quando si verifica il buffering iniziale utilizzando l&#39;accesso immediato.

## Imposta i tempi di buffering {#set-buffering-times}

Il `MediaPlayer` fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima della riproduzione iniziale, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo di buffer di riproduzione in corso.

1. Impostare l&#39;oggetto `BufferControlParameters`, che incapsula il tempo di buffer iniziale e i parametri di controllo del tempo di buffer di riproduzione:

       Questa classe fornisce due metodi di fabbrica:
   
   * Per impostare il tempo di buffer iniziale uguale al tempo del buffer di riproduzione:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Per impostare i tempi di buffer iniziali e di riproduzione:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Questi metodi generano un `IllegalArgumentException` se i parametri non sono validi, ad esempio quando:

   * Il tempo di buffer iniziale è inferiore a zero.
   * Il tempo di buffer iniziale è maggiore del tempo di buffer.

1. Per impostare i valori dei parametri del buffer, utilizzare questo metodo `MediaPlayer`:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizza questo metodo `MediaPlayer`:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Se l&#39;AVE non è in grado di impostare i valori specificati, il lettore multimediale immette lo stato `ERROR` con il codice di errore `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Ad esempio, per impostare il buffer iniziale a 2 secondi e il tempo del buffer di riproduzione a 30 secondi:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

L&#39;implementazione di riferimento di Primetime dimostra questa funzione; utilizzare le impostazioni dell&#39;applicazione per impostare i valori del buffer.