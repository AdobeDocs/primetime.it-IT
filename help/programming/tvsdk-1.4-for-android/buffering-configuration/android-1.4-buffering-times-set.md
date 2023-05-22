---
description: Per offrire un’esperienza di visualizzazione più fluida, TVSDK a volte archivia il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.
title: Impostare i tempi di buffering
exl-id: 4542d10a-b6f8-430d-8b9a-5a358d1c0e9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Buffering {#buffering}

Per offrire un’esperienza di visualizzazione più fluida, TVSDK a volte archivia il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.

TVSDK definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo iniziale del buffer entro il quale, prima dell’avvio della riproduzione del contenuto multimediale, deve essere di almeno 2 secondi. Dopo le chiamate dell’applicazione `play` ma prima dell’inizio della riproduzione, TVSDK memorizza in buffer il contenuto multimediale fino al momento iniziale per dare un inizio fluido quando inizia effettivamente la riproduzione.

È possibile modificare i tempi di buffer definendo nuovi criteri di buffering e modificare il momento in cui si verifica il buffering iniziale utilizzando l’opzione di attivazione immediata.

## Impostare i tempi di buffering {#set-buffering-times}

Il `MediaPlayer` fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering della riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima di iniziare la riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

1. Configurare `BufferControlParameters` oggetto, che incapsula i parametri di controllo del tempo del buffer iniziale e del tempo del buffer di riproduzione:

       Questa classe fornisce due metodi di fabbrica:
   
   * Per impostare il tempo del buffer iniziale uguale al tempo del buffer di riproduzione:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Per impostare i tempi del buffer iniziale e di riproduzione:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Questi metodi generano un `IllegalArgumentException` se i parametri non sono validi, ad esempio quando:

   * Il tempo del buffer iniziale è inferiore a zero.
   * Il tempo del buffer iniziale è maggiore del tempo del buffer.

1. Per impostare i valori dei parametri del buffer, utilizzare quanto segue `MediaPlayer` metodo:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizzare quanto segue `MediaPlayer` metodo:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Se l’AVE non è in grado di impostare i valori specificati, il lettore multimediale entra nel `ERROR` stato con il codice di errore `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Ad esempio, per impostare il buffer iniziale su 2 secondi e il tempo del buffer di riproduzione su 30 secondi:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

L’implementazione di riferimento di Primetime illustra questa funzione; utilizza le impostazioni dell’applicazione per impostare i valori del buffer.
