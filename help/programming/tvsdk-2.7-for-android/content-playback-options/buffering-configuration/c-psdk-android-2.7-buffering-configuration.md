---
description: Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare la modalità di buffer del lettore.
seo-description: Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare la modalità di buffer del lettore.
seo-title: Buffering
title: Buffering
uuid: 7f9f0deb-5f18-441d-b7a4-67c631a798f4
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Panoramica {#buffering-overview}

Per fornire un’esperienza di visualizzazione più fluida, TVSDK a volte carica il flusso video. È possibile configurare la modalità di buffer del lettore.

TVSDK definisce un buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale prima dell&#39;avvio della riproduzione del supporto, di almeno 2 secondi. Dopo le chiamate dell’applicazione `play`, ma prima dell’inizio della riproduzione, TVSDK esegue il buffer dei contenuti multimediali fino al tempo iniziale per dare un avvio corretto all’avvio effettivo della riproduzione.

È possibile modificare i tempi del buffer definendo nuovi criteri di buffering e modificare il momento in cui si verifica il buffering iniziale utilizzando immediatamente on.

## Criteri tempo di buffer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

A seconda dell’ambiente (incluso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare criteri di buffering diversi per il lettore, ad esempio modificare la durata minima del buffering iniziale e del buffering di riproduzione.

Dopo aver chiamato `play`, il lettore multimediale inizia la memorizzazione del video nel buffer. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l&#39;intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo aver inserito nel buffer i pochi secondi iniziali, la riproduzione inizia.

Durante il rendering del video, TVSDK continua a bufferizzare i nuovi frammenti fino a quando non viene memorizzato nel buffer la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza corrente del buffer scende al di sotto del tempo del buffer di riproduzione, il lettore scaricherà altri frammenti. Quando la lunghezza corrente del buffer è superiore di alcuni secondi al tempo del buffer di riproduzione, TVSDK interrompe il download dei frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è elevato, potrebbe fornire all&#39;utente un lungo tempo iniziale di buffering prima dell&#39;avvio. Ciò potrebbe fornire una riproduzione uniforme per un periodo di tempo più lungo; tuttavia, se le condizioni della rete non sono soddisfacenti, la riproduzione iniziale potrebbe essere ritardata.

Se si attiva l&#39;accesso immediato chiamando `prepareBuffer`, il buffer iniziale inizia in quel momento, invece di aspettare `play`.

## Impostare i tempi di buffering {#section_05CDD927869D47EBA1D2069B1416B2E4}

Sono `MediaPlayer` disponibili metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering della riproduzione.

>[!TIP]
>
>Se non impostate i parametri di controllo del buffer prima dell&#39;inizio della riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

1. Impostare l&#39; `BufferControlParameters` oggetto, che racchiude i parametri di tempo del buffer iniziale e di controllo del tempo del buffer di riproduzione.

   Questa classe fornisce i seguenti metodi factory:

   * Per impostare la durata iniziale del buffer uguale al tempo del buffer di riproduzione:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Per impostare i tempi di buffer iniziali e di riproduzione:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Se i parametri non sono validi, questi metodi generano `MediaPlayerException` `PSDKErrorCode.INVALID_ARGUMENT`con codice di errore, ad esempio quando vengono soddisfatte le seguenti condizioni:

   * Il tempo iniziale del buffer è inferiore a zero.
   * Il tempo iniziale del buffer è maggiore del tempo del buffer.


1. Per impostare i valori dei parametri del buffer, utilizzare questo `MediaPlayer` metodo:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Per ottenere i valori dei parametri del buffer correnti, utilizzate questo `MediaPlayer` metodo:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Ad esempio, per impostare il buffer iniziale su 5 secondi e il tempo del buffer di riproduzione su 30 secondi:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
