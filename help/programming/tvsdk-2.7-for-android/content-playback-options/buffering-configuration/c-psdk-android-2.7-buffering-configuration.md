---
description: Per offrire un’esperienza di visualizzazione più fluida, TVSDK a volte archivia il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.
title: Buffering
exl-id: f4df3084-376e-421c-aaa5-83de2815dabe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Panoramica {#buffering-overview}

Per offrire un’esperienza di visualizzazione più fluida, TVSDK a volte archivia il flusso video. Puoi configurare il modo in cui il lettore effettua il buffer.

TVSDK definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo iniziale del buffer di almeno 2 secondi prima dell’inizio della riproduzione del contenuto multimediale. Dopo le chiamate dell’applicazione `play`, ma prima dell’inizio della riproduzione, TVSDK memorizza in buffer il contenuto multimediale fino al momento iniziale per dare un inizio fluido quando inizia effettivamente la riproduzione.

È possibile modificare i tempi di buffer definendo nuovi criteri di buffering e modificare il momento in cui si verifica il buffering iniziale utilizzando l’opzione di attivazione immediata.

## Criteri tempo di buffering {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

A seconda dell’ambiente in uso (compreso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare criteri di buffering diversi per il lettore, ad esempio per modificare la durata minima del buffering iniziale e per la riproduzione in corso.

Dopo aver chiamato `play`, il lettore multimediale inizia a memorizzare il video nel buffering. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l’intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo aver inserito nel buffer i pochi secondi iniziali, inizia la riproduzione.

Durante il rendering del video, TVSDK continua a memorizzare nel buffer nuovi frammenti fino a quando non viene inserito nel buffer la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza del buffer corrente scende al di sotto del tempo del buffer di riproduzione, il lettore scarica altri frammenti. Quando la lunghezza del buffer corrente supera di alcuni secondi il tempo del buffer di riproduzione, TVSDK interrompe il download dei frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è alto, potrebbe assegnare all’utente un tempo di buffering iniziale lungo prima di iniziare. Questo potrebbe garantire una riproduzione fluida per un periodo di tempo più lungo; tuttavia, se le condizioni di rete sono scarse, la riproduzione iniziale potrebbe subire ritardi.

Se si abilita l&#39;attivazione immediata chiamando `prepareBuffer`, il buffering iniziale inizia in quel momento, invece di attendere `play`.

## Impostare i tempi di buffering {#section_05CDD927869D47EBA1D2069B1416B2E4}

Il `MediaPlayer` fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering della riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima di iniziare la riproduzione, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo del buffer di riproduzione in corso.

1. Configurare `BufferControlParameters` oggetto, che incapsula i parametri di controllo del tempo del buffer iniziale e del tempo del buffer di riproduzione.

   Questa classe fornisce i seguenti metodi di fabbrica:

   * Per impostare il tempo del buffer iniziale uguale al tempo del buffer di riproduzione:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Per impostare i tempi del buffer iniziale e di riproduzione:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Se i parametri non sono validi, questi metodi generano `MediaPlayerException` con codice di errore `PSDKErrorCode.INVALID_ARGUMENT`, ad esempio quando sono soddisfatte le seguenti condizioni:

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Ad esempio, per impostare il buffer iniziale su 5 secondi e il tempo del buffer di riproduzione su 30 secondi:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
