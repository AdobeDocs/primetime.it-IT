---
description: Per fornire un’esperienza di visualizzazione più fluida, a volte TVSDK carica il flusso video. Puoi configurare il buffer del lettore.
title: Buffering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Panoramica {#buffering-overview}

Per fornire un’esperienza di visualizzazione più fluida, a volte TVSDK carica il flusso video. Puoi configurare il buffer del lettore.

TVSDK definisce una lunghezza del buffer di riproduzione di almeno 30 secondi e un tempo di buffer iniziale prima che il supporto inizi la riproduzione, di almeno 2 secondi. Dopo che l&#39;applicazione chiama `play`, ma prima dell&#39;inizio della riproduzione, TVSDK carica il contenuto multimediale fino al tempo iniziale per dare un avvio fluido quando inizia effettivamente la riproduzione.

È possibile modificare i tempi di buffer definendo nuovi criteri di buffering e modificare quando si verifica il buffering iniziale utilizzando l&#39;accesso immediato.

## Criteri per il tempo di buffering {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

A seconda dell’ambiente (compreso il dispositivo, il sistema operativo o le condizioni di rete), è possibile impostare diversi criteri di buffering per il lettore, ad esempio la modifica della durata minima per il buffering iniziale e per il buffering di riproduzione continuo.

Dopo aver chiamato `play`, il lettore multimediale inizia a bufferizzare il video. Quando il lettore multimediale ha inserito nel buffer la quantità di video specificata dal tempo di buffer iniziale, la riproduzione inizia. Questo processo migliora il tempo di avvio perché il lettore non attende che l&#39;intero buffer di riproduzione si riempia prima di avviare la riproduzione. Al contrario, dopo il buffering dei pochi secondi iniziali, inizia la riproduzione.

Durante il rendering del video, TVSDK continua a creare un buffer per i nuovi frammenti fino a quando non viene bufferizzata la quantità specificata dal tempo del buffer di riproduzione. Se la lunghezza corrente del buffer scende al di sotto del tempo di riproduzione del buffer, il lettore scarica ulteriori frammenti. Una volta che la lunghezza corrente del buffer è superiore di alcuni secondi al tempo del buffer di riproduzione, TVSDK smetterà di scaricare i frammenti.

>[!TIP]
>
>Se il valore iniziale del buffer è elevato, potrebbe fornire all&#39;utente un lungo tempo iniziale di buffering prima dell&#39;avvio. Ciò potrebbe fornire una riproduzione uniforme per un periodo di tempo più lungo; tuttavia, se le condizioni di rete sono scadenti, la riproduzione iniziale potrebbe essere ritardata.

Se si attiva l&#39;accesso immediato chiamando `prepareBuffer`, il buffering iniziale inizia in quel momento, invece di attendere `play`.

## Imposta i tempi di buffering {#section_05CDD927869D47EBA1D2069B1416B2E4}

Il `MediaPlayer` fornisce metodi per impostare e ottenere il tempo di buffering iniziale e il tempo di buffering di riproduzione.

>[!TIP]
>
>Se non si impostano i parametri di controllo del buffer prima della riproduzione iniziale, il lettore multimediale utilizza per impostazione predefinita 2 secondi per il buffer iniziale e 30 secondi per il tempo di buffer di riproduzione in corso.

1. Impostare l&#39;oggetto `BufferControlParameters`, che incapsula il tempo di buffer iniziale e i parametri di controllo del tempo di buffer di riproduzione.

   Questa classe fornisce i seguenti metodi di fabbrica:

   * Per impostare il tempo di buffer iniziale uguale al tempo del buffer di riproduzione:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Per impostare i tempi di buffer iniziale e di riproduzione:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Se i parametri non sono validi, questi metodi generano `MediaPlayerException` con codice di errore `PSDKErrorCode.INVALID_ARGUMENT`, ad esempio quando sono soddisfatte le seguenti condizioni:

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Ad esempio, per impostare il buffer iniziale a 5 secondi e il tempo del buffer di riproduzione a 30 secondi:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
